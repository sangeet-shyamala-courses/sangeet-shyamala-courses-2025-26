<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Class Search</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; background: #f5f5f5; }
    input[type="text"] { width: 100%; padding: 10px; margin-bottom: 20px; border: 1px solid #ccc; border-radius: 5px; }
    .class-card { background: white; padding: 15px; margin-bottom: 10px; border-radius: 8px; box-shadow: 0 2px 5px rgba(0,0,0,0.1); }
    .title { font-size: 18px; font-weight: bold; }
    .details { font-size: 14px; color: #555; }
    .alert-box { background: #ffe5e5; border-left: 5px solid red; padding: 10px; margin-bottom: 20px; border-radius: 5px; }
  </style>
</head>
<body>

<h2>Search Classes</h2>
<input type="text" id="searchInput" placeholder="Type to search by class, teacher or day...">

<div id="alertBox" class="alert-box" style="display: none;"></div>
<div id="classList"></div>

<script>
  const classes = [
    { title: "Bharatnatyam - Meenakshi Rao", day: "Saturday, Sunday", time: "8:30 to 12:00pm", fee: "Rs.2800 (8 classes)" },
    { title: "Hindustani Vocal - Akansha", day: "Sat & Sun", time: "10:00 to 11:00pm", fee: "Rs.3000 / Rs.1200 (individual)" },
    { title: "Dance Fitness - Ajay Soni", day: "Mon, Wed, Fri", time: "6:15 to 7:15pm", fee: "Rs.3500/4500" },
    { title: "Yoga", day: "Tues & Thurs", time: "6:00 to 07:00pm", fee: "Rs.3000" },
    { title: "Karate - Tarun Chakravarty", day: "Mon & Thurs", time: "5:00 to 6:00pm", fee: "Rs.2000" },
    { title: "Creative Writing - Kiran Mishra", day: "Saturday, Sunday", time: "11:00 to 12:00pm / 3:00 to 4:00pm", fee: "Rs.2000 / Rs.700 (individual)" },
    { title: "Tabla - Bijoy Mandal", day: "Wed, Fri, Sat", time: "varied", fee: "Rs.2000 - 5500" },
    { title: "Ballet - Komal", day: "Saturday", time: "4:30 to 5:30pm", fee: "Rs.2500" },
    { title: "Odissi - Subrata Tripathy", day: "Thursday", time: "3:30 to 5:00pm", fee: "Rs.2000" },
    { title: "Piano & Voice - Kinneret", day: "Mon to Thurs", time: "9:00 to 6:45pm", fee: "Rs.1500 - 2000" },
    { title: "Vocal & Sitar - Sephali Maiti", day: "Tues & Fri", time: "5:00 to 6:00pm", fee: "Rs.2000" },
    { title: "Kathak - Deepti Gupta", day: "Tues, Wed, Sat, Sun", time: "multiple slots", fee: "Rs.2000 - 2300" },
    { title: "Painting - Gaurav Nagar", day: "Tues, Thurs, Sun", time: "varied", fee: "Rs.2000 - 4200" },
    { title: "Sculpture - Javed Hussain", day: "Sat & Sun", time: "10:30 to 12:30pm", fee: "Rs.2500" },
    { title: "Zumba - Shivani", day: "Thurs, Sat, Sun", time: "varied", fee: "Rs.2000 - 3500" }
  ];

  const listEl = document.getElementById('classList');
  const inputEl = document.getElementById('searchInput');
  const alertBox = document.getElementById('alertBox');

  function getCurrentDayTime() {
    const now = new Date();
    const days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
    return {
      day: days[now.getDay()],
      hour: now.getHours(),
      minute: now.getMinutes()
    };
  }

  function showClassAlert() {
    const { day, hour, minute } = getCurrentDayTime();
    const currentTime = hour + minute / 60;
    const matchingClasses = classes.filter(cls => {
      const lowerDay = cls.day.toLowerCase();
      if (!lowerDay.includes(day.toLowerCase())) return false;
      // Basic check if time range includes current time
      const match = cls.time.match(/(\d+):(\d+)\s*to\s*(\d+):(\d+)/);
      if (!match) return false;
      let [ , sh, sm, eh, em ] = match.map(Number);
      let start = sh + sm / 60;
      let end = eh + em / 60;
      return currentTime >= start && currentTime <= end;
    });

    if (matchingClasses.length > 0) {
      alertBox.style.display = 'block';
      alertBox.innerHTML = `<strong>Class Alert:</strong> Currently happening: <ul>${matchingClasses.map(c => `<li>${c.title}</li>`).join('')}</ul>`;
    } else {
      alertBox.style.display = 'none';
    }
  }

  function renderList(filter = "") {
    listEl.innerHTML = "";
    classes
      .filter(cls => cls.title.toLowerCase().includes(filter.toLowerCase()) || cls.day.toLowerCase().includes(filter.toLowerCase()))
      .forEach(cls => {
        const div = document.createElement('div');
        div.className = 'class-card';
        div.innerHTML = `<div class='title'>${cls.title}</div><div class='details'><strong>Day(s):</strong> ${cls.day} <br><strong>Time:</strong> ${cls.time} <br><strong>Fee:</strong> ${cls.fee}</div>`;
        listEl.appendChild(div);
      });
  }

  inputEl.addEventListener('input', () => renderList(inputEl.value));

  renderList();
  showClassAlert();
</script>

</body>
</html>
