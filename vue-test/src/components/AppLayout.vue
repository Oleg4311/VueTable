<style>
.content {
  display: grid;
  padding: 2rem;
  gap: 1.1rem;
}

.form-button {
  width: 8rem;
  height: 2.2rem;
  border-radius: 0.5rem;
  margin: auto;
  font-size: 1.2rem;
  font-weight: bold;
  border: 0.05rem solid var(--box-border);
  background-color: rgb(165, 201, 242);
  color: var(--prime-light-color);
  transition: 0.28s;
  cursor: pointer;
}

.form-button:hover {
  background-color: rgb(39, 216, 151);
  scale: 1.05;
}

.closeButton{
background-color: red;
}

</style>

<template>
  <div class="content">
    <button class="form-button" v-on:click="showForm = !showForm">Добавить</button>

    <AppTable
      :tableHeader="tableHeader"
      :tableBody="tableBody"
      :hiddenParameters="hiddenParameters"
    />

    <AppForm
      v-if="showForm"
      :tableHeader="tableHeader"
      :tableBody="tableBody"
      @submit="tableBody.push($event)"
      @hideForm="showForm = !showForm"
    />
  </div>
</template>

<script>
import AppTable from './AppTable.vue'
import AppForm from './AppForm.vue'

export default {
  name: 'AppLayout',
  components: {
    AppTable,
    AppForm
  },
  data () {
    return {
      showForm: false,
      tableHeader: [
        {
          id: 'name',
          title: 'Имя',
          sortable: true,
          sortType: { type: String },
          inputType: 'text'
        },
        {
          id: 'phone',
          title: 'Телефон',
          sortable: false,
          sortType: { type: String },
          inputType: 'tel'
        }
      ],
      tableBody: [
        {
          name: 'Марина',
          phone: '+7 941 123 21 42',
          parentId: 989,
          id: 999
        },
        {
          name: 'Петр',
          phone: '+7 941 123 21 52',
          parentId: 999,
          id: Math.random()
        },
        {
          name: 'Алексей',
          phone: '+7 941 123 21 62',
          parentId: null,
          id: 989
        },
        {
          name: 'Иван',
          phone: '+7 941 123 21 72',
          parentId: null,
          id: Math.random()
        },
        {
          name: 'Борис',
          phone: '+7 941 123 21 82',
          parentId: null,
          id: Math.random()
        }
      ],
      hiddenParameters: ['parentId', 'id']
    }
  },
  mounted () {
    const arrayString = localStorage.getItem('array')
    if (arrayString) {
      const array = JSON.parse(arrayString)
      this.tableBody = array
    }
  }
}
</script>
