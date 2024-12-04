<script setup>
import { ref, computed } from "vue";
const data = ref([
  { id: 1, name: "Banana" },
  { id: 2, name: "Apple" },
  { id: 3, name: "Orange" },
  { id: 4, name: "Mango" },
  { id: 5, name: "Pineapple" },
  { id: 6, name: "Grapes" },
  { id: 7, name: "Peach" },
]);
const sortKey = ref("");
const isAscending = ref(true);
const handleSort = () => {
  console.log(`Sorting by ${sortKey.value}`);
};

const sortedData = computed(() => {
  const sorted = [...data.value];
  if (sortKey.value) {
    console.log("test")
    sorted.sort((a, b) => {
      if (a[sortKey.value] < b[sortKey.value]) return isAscending.value ? -1 : 1;
      if (a[sortKey.value] > b[sortKey.value]) return isAscending.value ? 1 : -1;
      return 0;
    });
  }
  return sorted;
});
</script>

<template>

  <div class="container">
    <div class="container-grid">
      <div class="filter">
        <div class="display-filter">Filter</div>
        <div class="filter-select">
          <select class="select">
            <option>Select one</option>
            <option value="male">Male</option>
            <option value="female">Female</option>
            <option value="other">Other</option>
          </select>
        </div>
      </div>
      <div class="table">
        <div class="sort">
          <div class="label">Data</div>
          <div class="sort-dropdown">
            <div class="label">Sort by:</div>
            <select id="sort" v-model="sortKey" @change="handleSort" class="select">
              <option value="id">No.</option>
              <option value="name">Items</option>
            </select>
          </div>
        </div>

        <table class="rounded-table">
          <tbody>
            <tr v-if="sortedData.length === 0">
              <td colspan="2" class="no-data">No data available</td>
            </tr>
            <tr v-for="(item, index) in sortedData" :key="item.id" :class="index % 2 === 0 ? 'even-row' : 'odd-row'">
              <td>{{ item.name }}</td>

            </tr>
          </tbody>
        </table>
        <div class="pagination">
          <button class="pagination-button" disabled>
            &lt;
          </button>
          <span>1</span>
          <button class="pagination-button">
            &gt;
          </button>
        </div>
      </div>
    </div>
  </div>

</template>

<style scoped>
.container {
  margin-top: 90px;
  padding: 0 20px;
  flex-direction: column;

}

.container-grid {
  display: flex;
  width: 100%;
  gap: 20px;
  height: calc(100vh - 100px);

}


.filter {
  flex: 30%;
  background-color: #f0f0f0;
  padding: 20px;
}

.display-filter {
  display: flex;
  justify-content: center;
}

.filter-select {
  display: flex;
  justify-content: center;
  margin: 20px 0;
  width: 100%;
}

.select {
  width: 100%;
  padding: 10px 15px;
  font-size: 14px;
  color: #333;
  border: 1px solid #ccc;
  border-radius: 8px;
  background: #fff;
  cursor: pointer;
  outline: none;
  transition: all 0.3s ease;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.select:focus {
  border-color: #007bff;
  box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
}

.table {
  flex: 70%;
  padding: 0 20px;
}

.rounded-table {
  width: 100%;
  border-collapse: separate;
  border-spacing: 0;
  border: 1px solid #ddd;
  border-radius: 12px;
  overflow: hidden;
  height: calc(100% - 110px);
}

th,
td {
  padding: 10px;
  border: 1px solid #ddd;
  text-align: left;
}

button {
  margin-right: 5px;
  border-radius: 5px;
  height: 30px;
  cursor: pointer;
}

.even-row {
  background-color: #eaeaea;
}

.odd-row {

  background-color: #f9f9f9;
}

.sort {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
}

.sort-dropdown {
  margin-bottom: 10px;
  display: flex;
  align-items: center;
  gap: 5px;
}

.label {
  font-size: 14px;
  color: #333;
  width: 80px;
}

.pagination {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  gap: 10px;
  margin-top: 10px;
}

.pagination-button {
  padding: 5px 10px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.pagination-button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}

.pagination span {
  font-size: 14px;
}

@media (max-width: 768px) {
  .container-grid {
    flex-direction: column;
    gap: 10px;
    height: auto;
  }

  .filter {
    flex: 100%;
    padding: 10px;
  }

  .table {
    flex: 100%;
    padding: 0 10px;
  }

  .sort {
    flex-direction: column;
    align-items: flex-start;
    gap: 10px;
  }

  .rounded-table {
    height: auto;
  }

  th, td {
    font-size: 12px;
    padding: 8px;
  }

  .pagination {
    justify-content: center;
  }

  .select {
    font-size: 12px;
    padding: 8px 10px;
  }
  .label{
    text-decoration: underline;
  }
}

@media (max-width: 1024px) {
  .container-grid {
    flex-direction: column;
    gap: 15px;
    height: auto;
  }

  .sort-dropdown{
    display: none;
  }

  .filter {
    display: none;
  }

  .table {
    flex: 100%;
    padding: 0 15px;
  }

  th, td {
    font-size: 14px;
    padding: 10px;
  }

  .pagination {
    justify-content: center;
  }
}
</style>
