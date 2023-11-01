<template>
  <center>
  <div>
    <h2>Get all Menus</h2>
    <h4>จํานวนเมนูอาหาร {{ menus.length }}</h4>
    <p>
      <button class="button" v-on:click="navigateTo('/menu/create')">
        สร้างข้อมูลเมนูอาหาร<div class="hoverEffect"><div>
</div></div>
      </button>
    </p>

    <div v-for="menu in menus" v-bind:key="menu.id">
      <p>ชื่อเมนูอาหาร : {{ menu.name }}</p>
      <p>ประเภท : {{ menu.category }}</p>
      <p>ขนาด : {{ menu.size }}</p>
      <p>ราคา : {{ menu.price }} บาท</p>
      <p>
        <button class="botton" v-on:click="navigateTo('/menu/' + menu.id)">
          ดูข้อมูลเมนูอาหาร
        </button>

        <button class="botton" v-on:click="navigateTo('/menu/edit/' + menu.id)">
          แก้ไขข้อมูลเมนูอาหาร
        </button>

        <button class="button" v-on:click="deleteMenu(menu)">ลบข้อมูลเมนูอาหาร</button>
      </p>
      <hr />
    </div>
  </div>
</center>
</template>

<script>
import MenusService from "@/services/MenusService";
export default {
  data() {
    return {
      menus: [],
    };
  },
  async created() {
    try {
      this.menus = (await MenusService.index()).data;
    } catch (error) {
      console.log(error);
    }
  },
  methods: {
    navigateTo(route) {
      this.$router.push(route);
    },
    async deleteMenu(menu) {
      let result = confirm("Want of delete?")
      if (result) {
        try {
          await MenusService.delete(menu);
          this.refreshData();
        } catch (err) {
          console.log(err);
        }
      }
    },
    async refreshData() {
      this. menus = (await  MenusService.index()).data;
    },
  },
};
</script>


<style scoped>
button {
  outline: none;
  color: #DAA06D;
  padding: 0.5em;
  padding-left: 3em;
  padding-right: 2em;
  border: 2px dashed #DAA06D;
  border-radius: 15px;
  background-color: #EADDCA;
  box-shadow: 0 0 0 4px #EADDCA, 2px 2px 4px 2px rgba(0, 0, 0, 0.5);
  transition: .1s ease-in-out, .4s color;
}

button:active {
  transform: translateX(0.1em) translateY(0.1em);
  box-shadow: 0 0 0 4px #EADDCA, 1.5px 1.5px 2.5px 1.5px rgba(0, 0, 0, 0.5);
}



</style>