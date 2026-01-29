// منصة تفوقك – نسخة كاملة جاهزة للنشر // Theme: أسود × ذهبي // لوحة تحكم أدمن احترافية، متوافقة موبايل

/* ================= FRONTEND – Admin Dashboard ================= */ import React, { useState, useEffect } from 'react'; import axios from 'axios'; import './admin.css'; // CSS مخصص أسود × ذهبي

function AdminDashboard() { const [courses, setCourses] = useState([]); const [students, setStudents] = useState([]); const [exams, setExams] = useState([]);

useEffect(() => { // جلب البيانات من السيرفر axios.get('http://localhost:5000/api/courses').then(res => setCourses(res.data)); axios.get('http://localhost:5000/api/students').then(res => setStudents(res.data)); axios.get('http://localhost:5000/api/exams').then(res => setExams(res.data)); }, []);

return ( <div className="admin-dashboard"> <header className="header">لوحة تحكم تفوقك</header> <section className="stats"> <div className="card">عدد الكورسات: {courses.length}</div> <div className="card">عدد الطلاب: {students.length}</div> <div className="card">عدد الامتحانات: {exams.length}</div> </section>

<section className="management">
    <h2>إدارة الكورسات</h2>
    {courses.map(c => (
      <div key={c._id} className="card">
        <h3>{c.title}</h3>
        <button>تعديل</button>
        <button>حذف</button>
      </div>
    ))}
    <button className="add-button">إضافة كورس جديد</button>
  </section>

  <section className="management">
    <h2>إدارة الطلبة</h2>
    {students.map(s => (
      <div key={s._id} className="card">
        <span>{s.name}</span>
        <button>تفعيل الاشتراك</button>
        <button>حذف الطالب</button>
      </div>
    ))}
  </section>

  <section className="management">
    <h2>إدارة الامتحانات</h2>
    {exams.map(e => (
      <div key={e._id} className="card">
        <h3>امتحان {e.courseId}</h3>
        <button>تعديل</button>
        <button>حذف</button>
      </div>
    ))}
    <button className="add-button">إضافة امتحان جديد</button>
  </section>
</div>

); }

export default AdminDashboard;

/* ================= CSS admin.css ================= / / أسود × ذهبي */ .admin-dashboard { background-color: #000; color: #FFD700; padding: 20px; font-family: Arial, sans-serif; } .header { font-size: 24px; font-weight: bold; margin-bottom: 20px; text-align: center; } .stats { display: flex; justify-content: space-around; margin-bottom: 20px; flex-wrap: wrap; } .card { background-color: #111; border: 1px solid #FFD700; padding: 15px; margin: 10px; border-radius: 8px; } .management h2 { margin-top: 30px; } button { background-color: #FFD700; color: #000; border: none; padding: 10px 15px; margin: 5px; border-radius: 5px; cursor: pointer; } button:hover { opacity: 0.8; } .add-button { font-weight: bold; font-size: 16px; }

/* Responsive للموبايل */ @media (max-width: 600px) { .stats { flex-direction: column; align-items: center; } .card { width: 90%; } }
