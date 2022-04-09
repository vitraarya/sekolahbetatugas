<template>
  <section>
    <Header />
    <div class="py-4">
      <div class="container">
        <div
          class="
            title
            border-bottom
            d-flex
            align-items-center
            justify-content-between
            py-2
          "
        >
          <h5>Task</h5>
          <div class="d-flex align-items-center ms-auto">
            <input
              type="text"
              class="form-control"
              placeholder="Search"
              v-model="searchQuery"
            />
            <div class="d-flex align-items-center justify-content-end w-100">
              <span class="me-2">View As</span>
              <button
                class="btn btn-outline-secondary py-1 px-3"
                @click="isGrid = !isGrid"
              >
                {{ isGrid ? "Grid" : "List" }}
              </button>
            </div>
          </div>
        </div>
        <div class="list-task row">
          <CardItem
            v-for="(tasks, i) in resultQuery"
            :key="i"
            :tasks="tasks"
            :isGrid="isGrid"
          />
        </div>
        <div class="action py-2">
          <a
            href="#"
            class="add-button"
            v-if="!isCreating"
            @click="isCreating = !isCreating"
            >Add Task</a
          >
          <div class="add-card" v-else>
            <div class="card mb-2">
              <div class="card-body d-flex flex-column p-0">
                <input
                  class="form-control border-0 mb-2"
                  placeholder="Title"
                  type="text"
                />
                <textarea
                  class="form-control border-0 small"
                  placeholder="Description"
                  rows="3"
                ></textarea>
              </div>
            </div>
            <div class="button-wrapper d-flex">
              <button class="btn btn-outline-primary me-2">Save</button>
              <button
                class="btn btn-outline-danger"
                @click="isCreating = !isCreating"
              >
                Cancel
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
    <Footer />
  </section>
</template>
<script>
import CardItem from "@/components/Card/CardItem.vue";

export default {
  components: {
    CardItem,
  },
  data() {
    return {
      searchQuery: "",
      // Daftar task
      tasks: [
        {
          id: 1,
          title: "Task 1",
          description: "ini deskripsi 1",
          isDone: false,
        },
        {
          id: 2,
          title: "Task 2",
          description: "ini deskripsi 2",
          isDone: false,
        },
        {
          id: 3,
          title: "Task 3",
          description: "ini deskripsi 3",
          isDone: false,
        },
      ],
      
      isGrid: false,
      isCreating: false,
    };
  },
  computed: {
    resultQuery() {
      if (this.searchQuery) {
        return this.tasks.filter((item) => {
          return this.searchQuery
            .toLowerCase()
            .split("")
            .every((v) => item.title.toLowerCase().includes(v));
        });
      } else {
        return this.tasks;
      }
    },
  },
};
</script>
<style></style>
