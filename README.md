<input type="text" id="searchBox" placeholder="Search for a course..." onkeyup="searchCourse()" style="padding:10px;width:300px;margin-bottom:20px;">

<table id="courseTable">
  <tr><th>Course</th><th>Instructor</th><th>Days</th><th>Time</th><th>Fee</th></tr>
  <tr><td>Bharatnatyam</td><td>Meenakshi Rao</td><td>Sat & Sun</td><td>8:30–10:30am</td><td>₹2800</td></tr>
  <tr><td>Tabla</td><td>Bijoy Mandal</td><td>Wed & Fri</td><td>5:00–6:00pm</td><td>₹2000</td></tr>
  <tr><td>Zumba Fitness</td><td>Shivani</td><td>Thurs & Sun</td><td>5:00–6:00pm</td><td>₹3500</td></tr>
  <!-- Add more rows here -->
</table>

<script>
function searchCourse() {
  let input = document.getElementById("searchBox").value.toLowerCase();
  let rows = document.querySelectorAll("#courseTable tr");

  for (let i = 1; i < rows.length; i++) {
    let rowText = rows[i].innerText.toLowerCase();
    rows[i].style.display = rowText.includes(input) ? "" : "none";
  }
}
</script>
