import React, { useState } from "react";
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";
import { Table, TableBody, TableCell, TableHead, TableHeader, TableRow } from "@/components/ui/table";
import { PlusCircle, Settings } from "lucide-react";

const initialClasses = [
  {
    id: 1,
    category: "Dance",
    courseName: "Bharatnatyam",
    teacherName: "Meenakshi Rao",
    teacherImage: "https://via.placeholder.com/40",
    timing: "Saturday: 8:30 to 10:30am, Sunday: 9:30 to 11:30am, 11:00 to 12:00pm",
    room: "N/A",
    fee: "Rs.2800 (8 classes in a month)"
  },
  {
    id: 2,
    category: "Music",
    courseName: "Hindustani Vocal",
    teacherName: "Akansha",
    teacherImage: "https://via.placeholder.com/40",
    timing: "Sat & Sun (Kids): 10:00 to 11:00am, Sat & Sun (Adults): 10:00 to 11:00pm",
    room: "N/A",
    fee: "Rs.3000/-, Individual: Rs.1200/hr"
  },
  {
    id: 3,
    category: "Fitness",
    courseName: "Dance Fitness",
    teacherName: "Ajay Soni",
    teacherImage: "https://via.placeholder.com/40",
    timing: "Mon, Wed, Fri: 6:15 to 7:15pm",
    room: "N/A",
    fee: "Rs.3500 (8 classes), Rs.4500 (12 classes)"
  },
  {
    id: 4,
    category: "Fitness",
    courseName: "Yoga",
    teacherName: "",
    teacherImage: "https://via.placeholder.com/40",
    timing: "Tues & Thurs: 6:00 to 07:00pm",
    room: "N/A",
    fee: "Rs.3000 (8 classes)"
  }
  // Add other entries as needed following the same pattern
];

export default function ClassManagement() {
  const [classes, setClasses] = useState(initialClasses);
  const [search, setSearch] = useState("");

  const handleEdit = (id, field, value) => {
    setClasses(classes.map(cls => cls.id === id ? { ...cls, [field]: value } : cls));
  };

  const filteredClasses = classes.filter(cls =>
    cls.courseName.toLowerCase().includes(search.toLowerCase()) ||
    cls.teacherName.toLowerCase().includes(search.toLowerCase())
  );

  return (
    <div className="p-6 space-y-6">
      <div className="flex items-center justify-between">
        <h1 className="text-2xl font-bold">Class Management Dashboard</h1>
        <Button variant="outline">
          <Settings className="w-5 h-5 mr-2" /> Settings
        </Button>
      </div>

      <div className="flex items-center gap-4">
        <Input placeholder="Search by course or teacher..." value={search} onChange={(e) => setSearch(e.target.value)} />
        <Button>
          <PlusCircle className="w-5 h-5 mr-2" /> Add New Class
        </Button>
      </div>

      <Card>
        <CardContent>
          <Table>
            <TableHeader>
              <TableRow>
                <TableHead>Category</TableHead>
                <TableHead>Course Name</TableHead>
                <TableHead>Teacher</TableHead>
                <TableHead>Timing</TableHead>
                <TableHead>Room</TableHead>
                <TableHead>Fee</TableHead>
              </TableRow>
            </TableHeader>
            <TableBody>
              {filteredClasses.map(cls => (
                <TableRow key={cls.id}>
                  <TableCell>
                    <Input value={cls.category} onChange={e => handleEdit(cls.id, "category", e.target.value)} />
                  </TableCell>
                  <TableCell>
                    <Input value={cls.courseName} onChange={e => handleEdit(cls.id, "courseName", e.target.value)} />
                  </TableCell>
                  <TableCell className="flex items-center gap-2">
                    <img src={cls.teacherImage} alt={cls.teacherName} className="w-10 h-10 rounded-full" />
                    <Input value={cls.teacherName} onChange={e => handleEdit(cls.id, "teacherName", e.target.value)} />
                  </TableCell>
                  <TableCell>
                    <Input value={cls.timing} onChange={e => handleEdit(cls.id, "timing", e.target.value)} />
                  </TableCell>
                  <TableCell>
                    <Input value={cls.room} onChange={e => handleEdit(cls.id, "room", e.target.value)} />
                  </TableCell>
                  <TableCell>
                    <Input value={cls.fee || ""} onChange={e => handleEdit(cls.id, "fee", e.target.value)} />
                  </TableCell>
                </TableRow>
              ))}
            </TableBody>
          </Table>
        </CardContent>
      </Card>
    </div>
  );
}
