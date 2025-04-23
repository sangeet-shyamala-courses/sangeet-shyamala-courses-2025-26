<style>
  body {
    background: url('/mnt/data/colourful-ombre-background-blue-purple_218148-757.avif') no-repeat center center fixed;
    background-size: cover;
    font-family: Arial, sans-serif;
    padding: 20px;
    transition: background-color 0.5s ease, background-image 0.5s ease;
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
    transition: transform 0.3s;
  }
  .logo-container img:hover {
    transform: scale(1.05);
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
    transition: background 0.3s, transform 0.3s;
  }
  .category-menu span:hover {
    background: rgba(255,255,255,1);
    transform: translateY(-2px);
  }
  table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 20px;
    background-color: white;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    transition: box-shadow 0.3s;
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
  let matchCount = 0;
  rows.forEach(row => {
    const rowText = row.textContent.toLowerCase();
    if (rowText.includes(input)) {
      row.style.display = "";
      matchCount++;
    } else {
      row.style.display = "none";
    }
  });
  if (matchCount === 0 && !document.getElementById("noMatchRow")) {
    const tr = document.createElement("tr");
    tr.id = "noMatchRow";
    tr.innerHTML = `<td colspan="8" style="text-align:center; padding: 20px;">No matching courses found.</td>`;
    document.getElementById("tableBody").appendChild(tr);
  } else if (matchCount > 0 && document.getElementById("noMatchRow")) {
    document.getElementById("noMatchRow").remove();
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

const courseData = [...]; // (same as before)

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
