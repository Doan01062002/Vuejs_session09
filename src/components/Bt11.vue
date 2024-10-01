<template>
  <div>
    <section class="vh-100 gradient-custom">
      <div class="container py-5 h-100">
        <div class="row d-flex justify-content-center align-items-center h-100">
          <div class="col col-xl-10">
            <div class="card">
              <div class="card-body p-5">
                <h3 style="text-align: center; margin-bottom: 40px">
                  Quản lý công việc
                </h3>
                <form
                  @submit.prevent="addTask"
                  class="d-flex justify-content-center align-items-center mb-4"
                >
                  <div class="form-outline flex-fill">
                    <input
                      v-model="newTask"
                      type="text"
                      class="form-control"
                      :class="{ 'is-invalid': error }"
                    />
                    <label class="form-label">Thêm công việc</label>
                    <div v-if="error" class="invalid-feedback">{{ error }}</div>
                  </div>
                  <button type="submit" class="btn btn-info ms-2">Thêm</button>
                </form>

                <!-- Tabs content -->
                <div>
                  <ul class="list-group mb-0">
                    <li
                      v-for="task in tasks"
                      :key="task.id"
                      class="list-group-item d-flex align-items-center border-0 mb-2 rounded justify-content-between"
                      :style="{ backgroundColor: '#f4f6f7' }"
                    >
                      <div>
                        <input
                          class="form-check-input me-2"
                          type="checkbox"
                          v-model="task.completed"
                          @change="updateTaskStatus(task)"
                        />
                        <span
                          :class="{
                            'text-decoration-line-through': task.completed,
                          }"
                          >{{ task.name }}</span
                        >
                      </div>
                      <div>
                        <a
                          href="#!"
                          class="text-info"
                          @click="openEditModal(task)"
                        >
                          <i class="fas fa-pencil-alt me-3"></i>
                        </a>
                        <a
                          href="#!"
                          class="text-danger"
                          @click="openDeleteModal(task)"
                        >
                          <i class="fas fa-trash-alt"></i>
                        </a>
                      </div>
                    </li>
                  </ul>
                </div>
                <!-- Tabs content -->

                <div
                  v-if="completedTasks === tasks.length && tasks.length > 0"
                  class="alert alert-success mt-3"
                >
                  Hoàn thành công việc!
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Delete Modal -->
    <div v-if="showDeleteModal" class="modal">
      <div class="modal-content">
        <span class="close" @click="closeModal">&times;</span>
        <h2>Xác nhận</h2>
        <p>
          Bạn có xác nhận xóa công việc
          <code>{{ taskToDelete?.name }}</code> không?
        </p>
        <button @click="confirmDelete">Đồng ý</button>
        <button @click="closeModal">Hủy</button>
      </div>
    </div>

    <!-- Edit Modal -->
    <div v-if="showEditModal" class="modal">
      <div class="modal-content">
        <span class="close" @click="closeModal">&times;</span>
        <h2>Sửa công việc</h2>
        <input v-model="editedTaskName" class="form-control mb-3" />
        <button @click="updateTask">Cập nhật</button>
        <button @click="closeModal">Hủy</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, watch } from "vue";

// Task data management
const tasks = ref(JSON.parse(localStorage.getItem("tasks") || "[]"));
const newTask = ref("");
const error = ref(null);
const showDeleteModal = ref(false);
const showEditModal = ref(false);
const taskToDelete = ref(null);
const taskToEdit = ref(null);
const editedTaskName = ref("");

// Task validation and addition
const addTask = () => {
  if (!newTask.value.trim()) {
    error.value = "Tên công việc không được để trống.";
    return;
  }
  if (tasks.value.find((task) => task.name === newTask.value)) {
    error.value = "Tên công việc đã tồn tại.";
    return;
  }
  tasks.value.push({
    id: Date.now(),
    name: newTask.value.trim(),
    completed: false,
  });
  newTask.value = "";
  error.value = null;
  saveTasks();
};

// Delete task
const openDeleteModal = (task) => {
  taskToDelete.value = task;
  showDeleteModal.value = true;
};

const confirmDelete = () => {
  tasks.value = tasks.value.filter((task) => task.id !== taskToDelete.value.id);
  taskToDelete.value = null;
  showDeleteModal.value = false;
  saveTasks();
};

// Edit task
const openEditModal = (task) => {
  taskToEdit.value = task;
  editedTaskName.value = task.name;
  showEditModal.value = true;
};

const updateTask = () => {
  if (!editedTaskName.value.trim()) {
    error.value = "Tên công việc không được để trống.";
    return;
  }
  taskToEdit.value.name = editedTaskName.value.trim();
  taskToEdit.value = null;
  showEditModal.value = false;
  saveTasks();
};

// Update task status
const updateTaskStatus = (task) => {
  task.completed = !task.completed;
  saveTasks();
};

// Close modals
const closeModal = () => {
  showDeleteModal.value = false;
  showEditModal.value = false;
};

// Save tasks to localStorage
const saveTasks = () => {
  localStorage.setItem("tasks", JSON.stringify(tasks.value));
};

// Watch tasks to auto-save to localStorage
watch(tasks, saveTasks, { deep: true });

// Completed tasks count
const completedTasks = computed(
  () => tasks.value.filter((task) => task.completed).length
);
</script>

<style scoped>
.modal {
  display: block;
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.4);
}

.modal-content {
  background-color: #fefefe;
  margin: 15% auto;
  padding: 20px;
  border: 1px solid #888;
  width: 80%;
}

.close {
  color: #aaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.close:hover {
  color: black;
  cursor: pointer;
}

.text-decoration-line-through {
  text-decoration: line-through;
}
</style>
