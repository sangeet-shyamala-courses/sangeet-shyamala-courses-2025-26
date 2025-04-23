<style>
  body {
    background: url('/mnt/data/colourful-ombre-background-blue-purple_218148-757.avif') no-repeat center center fixed;
    background-size: cover;
    font-family: Arial, sans-serif;
    padding: 20px;
    transition: background-color 0.5s ease;
  }
  h1 {
    text-align: center;
    margin-bottom: 10px;
  }
  .logo-container {
    text-align: center;
    margin-bottom: 20px;
  }
  .logo-container img {
    max-width: 200px;
    height: auto;
    cursor: pointer;
  }
  .category-menu {
    text-align: center;
    margin-bottom: 20px;
    font-size: 18px;
  }
  .category-menu span {
    margin: 0 10px;
    cursor: pointer;
    padding: 8px 16px;
    background: rgba(255,255,255,0.8);
    border-radius: 8px;
    transition: background 0.3s;
  }
  .category-menu span:hover {
    background: rgba(255,255,255,1);
  }
  table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 20px;
    background-color: white;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  }
  th, td {
    border: 1px solid #ccc;
    padding: 12px;
    text-align: left;
  }
  th {
    background-color: #f7f9fc;
  }
  tr:hover {
    background-color: #eef3f7;
  }
</style>

<div class="logo-container">
  <img src="/mnt/data/ShyamalaLogo-14 (1).png" alt="Sangeet Shyamala Logo" onclick="changeLogo()">
</div>

<h1>Sangeet Shyamala Course Schedule</h1>

<div class="category-menu">
  <span onclick="filterCategory('music')">🎵 Music Classes</span>
  <span onclick="filterCategory('dance')">💃 Dance Classes</span>
  <span onclick="filterCategory('fitness')">🧘 Fitness Classes</span>
  <span onclick="filterCategory('art')">🎨 Art Classes</span>
  <span onclick="filterCategory('writing')">✍️ Writing Classes</span>
</div>

<div style="text-align:center; margin-bottom: 20px;">
  <label for="bgColorPicker">Change Background Color:</label>
  <input type="color" id="bgColorPicker" onchange="document.body.style.backgroundColor = this.value">
</div>

<input type="text" id="searchBox" placeholder="Search for a course..." onkeyup="searchCourse()" style="padding:10px;width:300px;margin-bottom:20px;">
<button onclick="addNewRow()" style="padding:10px 20px;margin-left:10px;">Add New Row</button>

<table id="courseTable">
  <thead>
    <tr>
      <th>Course</th>
      <th>Instructor</th>
      <th>Days</th>
      <th>Time</th>
      <th>Fee</th>
      <th>Room No.</th>
      <th>Type</th>
      <th>Actions</th>
    </tr>
  </thead>
  <tbody id="tableBody">
  </tbody>
</table>

<script>
function searchCourse() {
  let input = document.getElementById("searchBox").value.toLowerCase();
  let rows = document.querySelectorAll("#courseTable tbody tr");
  for (let i = 0; i < rows.length; i++) {
    let rowText = rows[i].innerText.toLowerCase();
    rows[i].style.display = rowText.includes(input) ? "" : "none";
  }
}

function addNewRow() {
  const table = document.getElementById("tableBody");
  const newRow = document.createElement("tr");
  newRow.innerHTML = `
    <td contenteditable="true">New Course</td>
    <td contenteditable="true">Instructor</td>
    <td contenteditable="true">Days</td>
    <td contenteditable="true">Time</td>
    <td contenteditable="true">Fee</td>
    <td contenteditable="true">Room No.</td>
    <td contenteditable="true">Group/Individual</td>
    <td><button onclick="alert('Changes saved!')">Save</button></td>
  `;
  table.appendChild(newRow);
}

function changeLogo() {
  const fileInput = document.createElement("input");
  fileInput.type = "file";
  fileInput.accept = "image/*";
  fileInput.onchange = (e) => {
    const file = e.target.files[0];
    const reader = new FileReader();
    reader.onload = (event) => {
      document.querySelector(".logo-container img").src = event.target.result;
    };
    reader.readAsDataURL(file);
  };
  fileInput.click();
}

function filterCategory(type) {
  const rows = document.querySelectorAll("#tableBody tr");
  rows.forEach(row => {
    const course = row.cells[0]?.textContent.toLowerCase() || "";
    const matches = {
      music: /vocal|tabla|piano|sitar|voice/.test(course),
      dance: /dance|ballet|kathak|odissi|bharatnatyam|salsa/.test(course),
      fitness: /fitness|yoga|karate|zumba/.test(course),
      art: /painting|sculpture|art/.test(course),
      writing: /writing/.test(course),
    };
    row.style.display = matches[type] ? "" : "none";
  });
}

const courseData = [
  ["Bharatnatyam", "Meenakshi Rao", "Saturday, Sunday", "8:30 to 10:30am, 9:30 to 11:30am, 11:00 to 12:00pm", "₹2800 (8 classes/month)", "", "Group"],
  ["Hindustani Vocal", "Akansha", "Sat & Sun", "10:00 to 11:00am", "₹3000, ₹1200/hr (individual)", "", "Both"],
  ["Dance Fitness", "Ajay Soni", "Mon, Wed, Fri", "6:15 to 7:15pm", "₹3500 (8 classes), ₹4500 (12 classes)", "", "Group"],
  ["Yoga", "—", "Tues & Thurs", "6:00 to 7:00pm", "₹3000 (8 classes/month)", "", "Group"],
  ["Karate", "Tarun Chakravarty", "Mon & Thurs", "5:00 to 6:00pm", "₹2000 (8 classes/month)", "", "Group"],
  ["Creative Writing", "Kiran Mishra", "Saturday, Sunday", "11:00 to 12:00pm, 3:00 to 4:00pm", "₹2000 (4 classes), ₹700/hr, ₹1000/hr", "", "Both"],
  ["Tabla", "Bijoy Mandal", "Wed & Fri, Sat", "5:00 to 6:00pm, 10:30 to 12:00pm", "₹2000, ₹4500 (8 classes/month)", "", "Both"],
  ["Ballet", "Komal", "Thurs & Sat", "4:00 to 5:00pm, 5:00 to 6:00pm", "₹3000 (4 classes), ₹5500 (8 classes)", "", "Group"],
  ["Bharatnatyam", "Arupa Lahiry", "Saturday, Sunday", "4:30 to 5:30pm, 10:30 to 11:30am", "₹2500", "", "Group"],
  ["Odissi", "Subrata Tripathy", "Thursday", "3:30 to 5:00pm", "₹2000 (4 classes/month)", "", "Group"],
  ["Piano & Voice", "Kinneret Prabhudas", "Mon to Thurs", "9:00 to 6:45pm", "₹2000 (45 min), ₹1500 (30 min)", "", "Individual"],
  ["Vocal & Sitar", "Sephali Maiti", "Tues & Fri", "5:00 to 6:00pm", "₹2000", "", "Group"],
  ["Voice & Piano", "Subhiksha A.", "Fri", "—", "₹1200 (40 min)", "", "Individual"],
  ["Kathak", "Deepti Gupta", "Tues & Wed (Adv.), Sat & Sun (Adv.)", "5:00 to 6:00pm, 1:30 to 2:30pm", "₹2000 (kids), ₹2300 (adults)", "", "Group"],
  ["Sculpture", "Javed Hussain", "Sat & Sun", "10:30 to 12:30pm", "₹2500 (8 classes/month)", "", "Group"],
  ["Zumba Fitness", "Shivani", "Thurs & Sat", "5:00 to 6:00pm", "₹2000 (4 classes), ₹3500 (8 classes)", "", "Group"],
  ["Sitar", "—", "Tues", "4:00 to 5:00pm", "₹1500/class (individual), ₹4000 group", "", "Both"]
];

window.onload = function populateTable() {
  const table = document.getElementById("tableBody");
  courseData.forEach(row => {
    const tr = document.createElement("tr");
    row.forEach(cell => {
      const td = document.createElement("td");
      td.textContent = cell;
      td.contentEditable = true;
      tr.appendChild(td);
    });
    const action = document.createElement("td");
    action.innerHTML = '<button onclick="alert(\'Changes saved!\')">Save</button>';
    tr.appendChild(action);
    table.appendChild(tr);
  });
};
</script>
