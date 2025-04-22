<style>
  body {
    background: linear-gradient(to right, #f0f2f5, #d9e2ec);
    font-family: Arial, sans-serif;
    padding: 20px;
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
  <tbody id="tableBody">
    <!-- Course rows are editable and can be extended dynamically -->
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

const courseData = [
  ["Bharatnatyam", "Meenakshi Rao", "Saturday, Sunday", "8:30 to 10:30am, 9:30 to 11:30am, 11:00 to 12:00pm", "₹2800 (8 classes/month)", "Room 101"],
  ["Hindustani Vocal", "Akansha", "Sat & Sun", "10:00 to 11:00am", "₹3000, ₹1200/hr (individual)", "Room 102"],
  ["Dance Fitness", "Ajay Soni", "Mon, Wed, Fri", "6:15 to 7:15pm", "₹3500 (8 classes), ₹4500 (12 classes)", "Room 103"],
  ["Yoga", "—", "Tues & Thurs", "6:00 to 7:00pm", "₹3000 (8 classes/month)", "Room 104"],
  ["Karate", "Tarun Chakravarty", "Mon & Thurs", "5:00 to 6:00pm", "₹2000 (8 classes/month)", "Room 105"],
  ["Creative Writing", "Kiran Mishra", "Saturday, Sunday", "11:00 to 12:00pm, 3:00 to 4:00pm", "₹2000 (4 classes), ₹700/hr, ₹1000/hr", "Room 106"],
  ["Tabla", "Bijoy Mandal", "Wed & Fri, Sat", "5:00 to 6:00pm, 10:30 to 12:00pm", "₹2000, ₹4500 (8 classes/month)", "Room 107"],
  ["Ballet", "Komal", "Thurs & Sat", "4:00 to 5:00pm, 5:00 to 6:00pm", "₹3000 (4 classes), ₹5500 (8 classes)", "Room 108"],
  ["Bharatnatyam", "Arupa Lahiry", "Saturday, Sunday", "4:30 to 5:30pm, 10:30 to 11:30am", "₹2500", "Room 109"],
  ["Odissi", "Subrata Tripathy", "Thursday", "3:30 to 5:00pm", "₹2000 (4 classes/month)", "Room 110"],
  ["Piano & Voice", "Kinneret Prabhudas", "Mon to Thurs", "9:00 to 6:45pm", "₹2000 (45 min), ₹1500 (30 min)", "Room 111"],
  ["Vocal & Sitar", "Sephali Maiti", "Tues & Fri", "5:00 to 6:00pm", "₹2000", "Room 112"],
  ["Voice & Piano", "Subhiksha A.", "Fri", "—", "₹1200 (40 min)", "Room 113"],
  ["Kathak", "Deepti Gupta", "Tues & Wed (Adv.), Sat & Sun (Adv.)", "5:00 to 6:00pm, 1:30 to 2:30pm", "₹2000 (kids), ₹2300 (adults)", "Room 114"],
  ["Sculpture", "Javed Hussain", "Sat & Sun", "10:30 to 12:30pm", "₹2500 (8 classes/month)", "Room 115"],
  ["Zumba Fitness", "Shivani", "Thurs & Sat", "5:00 to 6:00pm", "₹2000 (4 classes), ₹3500 (8 classes)", "Room 116"]
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
