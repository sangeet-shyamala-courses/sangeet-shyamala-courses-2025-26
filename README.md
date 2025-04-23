<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Class Management Dashboard</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
    }
    .table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 20px;
    }
    .table th, .table td {
      border: 1px solid #ddd;
      padding: 8px;
    }
    .table th {
      background-color: #f2f2f2;
    }
    .search-input {
      padding: 8px;
      margin-bottom: 20px;
      width: 300px;
    }
    .teacher-img {
      width: 40px;
      height: 40px;
      border-radius: 50%;
      vertical-align: middle;
      margin-right: 10px;
    }
    .editable {
      width: 100%;
      border: none;
      background: transparent;
    }
  </style>
</head>
<body>
  <h1>Class Management Dashboard</h1>

  <input type="text" class="search-input" id="search" placeholder="Search by course or teacher..." onkeyup="filterTable()" />

  <table class="table" id="classTable">
    <thead>
      <tr>
        <th>Category</th>
        <th>Course Name</th>
        <th>Teacher</th>
        <th>Timing</th>
        <th>Room</th>
        <th>Fee</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><input class="editable" value="Dance"></td>
        <td><input class="editable" value="Bharatnatyam"></td>
        <td><img src="https://via.placeholder.com/40" class="teacher-img"><input class="editable" value="Meenakshi Rao"></td>
        <td><input class="editable" value="Saturday: 8:30 to 10:30am, Sunday: 9:30 to 11:30am, 11:00 to 12:00pm"></td>
        <td><input class="editable" value="N/A"></td>
        <td><input class="editable" value="Rs.2800 (8 classes in a month)"></td>
      </tr>
      <tr>
        <td><input class="editable" value="Music"></td>
        <td><input class="editable" value="Hindustani Vocal"></td>
        <td><img src="https://via.placeholder.com/40" class="teacher-img"><input class="editable" value="Akansha"></td>
        <td><input class="editable" value="Sat & Sun (Kids): 10:00 to 11:00am, Sat & Sun (Adults): 10:00 to 11:00pm"></td>
        <td><input class="editable" value="N/A"></td>
        <td><input class="editable" value="Rs.3000/-, Individual: Rs.1200/hr"></td>
      </tr>
      <tr>
        <td><input class="editable" value="Fitness"></td>
        <td><input class="editable" value="Dance Fitness"></td>
        <td><img src="https://via.placeholder.com/40" class="teacher-img"><input class="editable" value="Ajay Soni"></td>
        <td><input class="editable" value="Mon, Wed, Fri: 6:15 to 7:15pm"></td>
        <td><input class="editable" value="N/A"></td>
        <td><input class="editable" value="Rs.3500 (8 classes), Rs.4500 (12 classes)"></td>
      </tr>
      <tr>
        <td><input class="editable" value="Fitness"></td>
        <td><input class="editable" value="Yoga"></td>
        <td><img src="https://via.placeholder.com/40" class="teacher-img"><input class="editable" value=""></td>
        <td><input class="editable" value="Tues & Thurs: 6:00 to 07:00pm"></td>
        <td><input class="editable" value="N/A"></td>
        <td><input class="editable" value="Rs.3000 (8 classes)"></td>
      </tr>
    </tbody>
  </table>

  <script>
    function filterTable() {
      const input = document.getElementById("search");
      const filter = input.value.toLowerCase();
      const table = document.getElementById("classTable");
      const trs = table.getElementsByTagName("tr");

      for (let i = 1; i < trs.length; i++) {
        let show = false;
        const tds = trs[i].getElementsByTagName("td");
        for (let j = 0; j < tds.length; j++) {
          const input = tds[j].getElementsByTagName("input")[0];
          if (input && input.value.toLowerCase().includes(filter)) {
            show = true;
            break;
          }
        }
        trs[i].style.display = show ? "" : "none";
      }
    }
  </script>
</body>
</html>
