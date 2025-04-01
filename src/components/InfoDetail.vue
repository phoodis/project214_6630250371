<template>
  <div class="card">
    <div class="card-body">
      <h2>My Information</h2>
      <img src="/images/nisitPic.jpg" alt="My Picture" class="profile-img" />

      <div v-if="user">
        <p><strong>Student ID:</strong> {{ user.student_id }}</p>
        <p><strong>Full Name:</strong> {{ user.first_name }} {{ user.last_name }}</p>
        <p><strong>Faculty:</strong> {{ user.faculty }}</p>
        <p><strong>Department:</strong> {{ user.department }}</p>
        <p><strong>Year:</strong> {{ user.year }}</p>
        <p><strong>Email:</strong> {{ user.email }}</p>

        <button @click="editMode = true" v-if="!editMode" class="btn edit-btn">Edit</button>

        <form v-if="editMode" @submit.prevent="updateInfo" class="edit-form">
          <label>Student ID</label>
          <input type="text" v-model.trim="user.student_id" required />

          <label>Full Name</label>
          <input type="text" v-model.trim="user.first_name" placeholder="First Name" required />
          <input type="text" v-model.trim="user.last_name" placeholder="Last Name" required />

          <label>Faculty</label>
          <select v-model="user.faculty" required>
            <option value="Science">Science</option>
            <option value="Management">Management</option>
            <option value="Engineering">Engineering</option>
            <option value="Maritime Commerce">Maritime Commerce</option>
          </select>

          <label>Year</label>
          <select v-model="user.year" required>
            <option value="1">Year 1</option>
            <option value="2">Year 2</option>
            <option value="3">Year 3</option>
            <option value="4">Year 4</option>
            <option value="5">Beyond Year 4</option>
          </select>

          <label>Email</label>
          <input type="email" v-model.trim="user.email" required />

          <div class="form-actions">
            <button type="submit" class="btn save-btn">Save</button>
            <button type="button" class="btn cancel-btn" @click="editMode = false">Cancel</button>
          </div>
        </form>

        <h3>Grades</h3>
        <table class="grade-table">
          <thead>
            <tr>
              <th>Course Code</th>
              <th>Course Name</th>
              <th>Credits</th>
              <th>Grade</th>
              <th>Actions</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(course, index) in user.courses" :key="course.code">
              <td>{{ course.code }}</td>
              <td>{{ course.name }}</td>
              <td>{{ course.credits }}</td>
              <td v-if="!course.editMode">{{ course.grade }}</td>
              <td v-else>
                <input type="text" v-model.trim="course.tempGrade" />
              </td>
              <td>
                <button v-if="!course.editMode" @click="editGrade(index)" class="btn small-btn">Edit</button>
                <button v-else @click="saveGrade(index)" class="btn small-btn">Save</button>
                <button v-if="course.editMode" @click="cancelEdit(index)" class="btn small-btn cancel-btn">Cancel</button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>

      <p v-else>Downloading...</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      user: null,
      editMode: false,
    };
  },
  mounted() {
    fetch("http://localhost:3000/user")
      .then((res) => res.json())
      .then((data) => {
        if (Array.isArray(data) && data.length > 0) {
          this.user = data[0];
          if (Array.isArray(this.user.courses)) {
            this.user.courses.forEach(course => {
              course.tempGrade = course.grade;
              course.editMode = false;
            });
          } else {
            this.user.courses = [];
          }
        }
      })
      .catch((err) => console.error("❌ Error fetching data:", err));
  },
  methods: {
    updateInfo() {
      alert("✅ ข้อมูลอัปเดตแล้ว!");
      this.editMode = false;
    },
    editGrade(index) {
      this.user.courses[index].editMode = true;
    },
    saveGrade(index) {
      this.user.courses[index].grade = this.user.courses[index].tempGrade;
      this.user.courses[index].editMode = false;
    },
    cancelEdit(index) {
      this.user.courses[index].tempGrade = this.user.courses[index].grade;
      this.user.courses[index].editMode = false;
    },
  }
};
</script>

<style>
body {
  font-family: Arial, sans-serif;
  background-color: #f4f4f4;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  margin: 0;
}

.card {
  background: #fffdf0;
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  text-align: center;
  max-width: 600px;
  width: 100%;
}

.profile-img {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  object-fit: cover;
  margin-top: 15px;
  border: 3px solid #0073e6;
}

.edit-form input,
.edit-form select {
  width: 100%;
  padding: 8px;
  margin: 5px 0;
  border-radius: 5px;
  border: 1px solid #ccc;
}

.form-actions {
  display: flex;
  justify-content: center;
  gap: 10px;
}

.btn {
  padding: 8px 12px;
  border: none;
  cursor: pointer;
  border-radius: 5px;
}

.edit-btn {
  background-color: #0073e6;
  color: white;
}

.save-btn {
  background-color: #28a745;
  color: white;
}

.cancel-btn {
  background-color: #dc3545;
  color: white;
}

.small-btn {
  padding: 5px 10px;
  font-size: 0.9em;
}

.grade-table {
  width: 100%;
  margin-top: 20px;
  border-collapse: collapse;
}

.grade-table th,
.grade-table td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: center;
}

.grade-table th {
  background-color: #0073e6;
  color: white;
}
</style>
