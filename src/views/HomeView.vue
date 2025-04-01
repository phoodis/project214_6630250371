<script setup>
</script>

<template>
  <main>
    <section class="container">
      <h1>Welcome to My Portfolio! 🚀</h1>
      <p>
        This is my first portfolio project, created using 
        <strong>Vue.js</strong> in the 
        <strong>Practicum in Software Development</strong> course.
      </p>
      <p>
        In this portfolio, you can find my information, which can be edited and saved in 
        <code>info.json</code>.
      </p>
      <img src="/images/bussinessman.jpg" alt="Cool guy" title="Welcome!!" class="profile-img" />
    </section>
  </main>
</template>

<style>
/* ตั้งค่าพื้นฐานของหน้าเว็บ */
body {
  font-family: Arial, sans-serif;
  background-color: #f4f4f4;
  color: #333;
  margin: 0;
  padding: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
}

/* กล่องเนื้อหา */
.container {
  background: white;
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  text-align: center;
  max-width: 600px;
}

h1 {
  color: #0073e6;
}

p {
  font-size: 1.1em;
  line-height: 1.6;
}

code {
  background: #eee;
  padding: 3px 6px;
  border-radius: 4px;
  font-family: "Courier New", monospace;
}

/* รูปภาพโปรไฟล์ */
.profile-img {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  object-fit: cover;
  margin-top: 15px;
  border: 3px solid #0073e6;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  transition: transform 0.3s ease, box-shadow 0.3s ease; /* เพิ่ม transition สำหรับการเปลี่ยนแปลง */
}

.profile-img:hover {
  transform: scale(1.2); /* ขยายขนาด 1.2 เท่าเมื่อ hover */
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.3); /* เพิ่มเงาเมื่อ hover */
}
</style>
