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
      <th>Actions</th>
    </tr>
  </thead>
  <tbody>
    <tr><td contenteditable="true">Bharatnatyam</td><td contenteditable="true">Meenakshi Rao</td><td contenteditable="true">Saturday, Sunday</td><td contenteditable="true">8:30 to 10:30am, 9:30 to 11:30am, 11:00 to 12:00pm</td><td contenteditable="true">₹2800 (8 classes/month)</td><td contenteditable="true">Room 101</td><td><button onclick="alert('Changes saved!')">Save</button></td></tr>
    <tr><td contenteditable="true">Hindustani Vocal</td><td contenteditable="true">Akansha</td><td contenteditable="true">Sat & Sun</td><td contenteditable="true">10:00 to 11:00am</td><td contenteditable="true">₹3000, ₹1200/hr (individual)</td><td contenteditable="true">Room 102</td><td><button onclick="alert('Changes saved!')">Save</button></td></tr>
    <tr><td contenteditable="true">Dance Fitness</td><td contenteditable="true">Ajay Soni</td><td contenteditable="true">Mon, Wed, Fri</td><td contenteditable="true">6:15 to 7:15pm</td><td contenteditable="true">₹3500 (8 classes), ₹4500 (12 classes)</td><td contenteditable="true">Room 103</td><td><button onclick="alert('Changes saved!')">Save</button></td></tr>
    <tr><td contenteditable="true">Yoga</td><td contenteditable="true">—</td><td contenteditable="true">Tues & Thurs</td><td contenteditable="true">6:00 to 7:00pm</td><td contenteditable="true">₹3000 (8 classes/month)</td><td contenteditable="true">Room 104</td><td><button onclick="alert('Changes saved!')">Save</button></td></tr>
    <tr><td contenteditable="true">Karate</td><td contenteditable="true">Tarun Chakravarty</td><td contenteditable="true">Mon & Thurs</td><td contenteditable="true">5:00 to 6:00pm</td><td contenteditable="true">₹2000 (8 classes/month)</td><td contenteditable="true">Room 105</td><td><button onclick="alert('Changes saved!')">Save</button></td></tr>
    <tr><td contenteditable="true">Creative Writing</td><td contenteditable="true">Kiran Mishra</td><td contenteditable="true">Saturday, Sunday</td><td contenteditable="true">11:00 to 12:00pm, 3:00 to 4:00pm</td><td contenteditable="true">₹2000 (4 classes), ₹700/hr, ₹1000/hr</td><td contenteditable="true">Room 106</td><td><button onclick="alert('Changes saved!')">Save</button></td></tr>
    <tr><td contenteditable="true">Tabla</td><td contenteditable="true">Bijoy Mandal</td><td contenteditable="true">Wed & Fri, Sat</td><td contenteditable="true">5:00 to 6:00pm, 10:30 to 12:00pm</td><td contenteditable="true">₹2000, ₹4500 (8 classes/month)</td><td contenteditable="true">Room 107</td><td><button onclick="alert('Changes saved!')">Save</button></td></tr>
    <tr><td contenteditable="true">Ballet</td><td contenteditable="true">Komal</td><td contenteditable="true">Thurs & Sat</td><td contenteditable="true">4:00 to 5:00pm, 5:00 to 6:00pm</td><td contenteditable="true">₹3000 (4 classes), ₹5500 (8 classes)</td><td contenteditable="true">Room 108</td><td><button onclick="alert('Changes saved!')">Save</button></td></tr>
    <tr><td contenteditable="true">Bharatnatyam</td><td contenteditable="true">Arupa Lahiry</td><td contenteditable="true">Saturday, Sunday</td><td contenteditable="true">4:30 to 5:30pm, 10:30 to 11:30am</td><td contenteditable="true">₹2500</td><td contenteditable="true">Room 109</td><td><button onclick="alert('Changes saved!')">Save</button></td></tr>
    <tr><td contenteditable="true">Odissi</td><td contenteditable="true">Subrata Tripathy</td><td contenteditable="true">Thursday</td><td contenteditable="true">3:30 to 5:00pm</td><td contenteditable="true">₹2000 (4 classes/month)</td><td contenteditable="true">Room 110</td><td><button onclick="alert('Changes saved!')">Save</button></td></tr>
    <tr><td contenteditable="true">Piano & Voice</td><td contenteditable="true">Kinneret Prabhudas</td><td contenteditable="true">Mon to Thurs</td><td contenteditable="true">9:00 to 6:45pm</td><td contenteditable="true">₹2000 (45 min), ₹1500 (30 min)</td><td contenteditable="true">Room 111</td><td><button onclick="alert('Changes saved!')">Save</button></td></tr>
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
  const table = document.querySelector("#courseTable tbody");
  const newRow = document.createElement("tr");
  newRow.innerHTML = `
    <td contenteditable="true">New Course</td>
    <td contenteditable="true">Instructor</td>
    <td contenteditable="true">Days</td>
    <td contenteditable="true">Time</td>
    <td contenteditable="true">Fee</td>
    <td contenteditable="true">Room No.</td>
    <td><button onclick="alert('Changes saved!')">Save</button></td>
  `;
  table.appendChild(newRow);
}
</script>
