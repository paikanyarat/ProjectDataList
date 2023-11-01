<template>
  <center>
    <div>
      <h1>Get Menu</h1>
      <p>ชื่อเมนู : <input type="text" v-model="menu.name" /></p>
      <p>ราคา : <input type="text" v-model="menu.price" /></p>
      <p>ขนาด : <input type="text" v-model="menu.size" /></p>
      <p>ประเภท : <input type="text" v-model="menu.category" /></p>
      <p>รายละเอียด: <input type="text" v-model="menu.description" /></p>
      <p>ส่วนประกอบ : <input type="text" v-model="menu.ingredients" /></p>
    </div>
  </center>
  </template>
  <script>
  import MenusService from "@/services/MenusService";
  export default {
    data() {
      return {
        menu: "",
      };
    },
    async created() {
      try {
        let menuId = this.$route.params.menusId;
        this.menu = (await MenusService.show(menuId)).data;
      } catch (error) {
        console.log(error);
      }
    },
  };
  </script>
<style scoped>
.button {
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

.button:active {
  transform: translateX(0.1em) translateY(0.1em);
  box-shadow: 0 0 0 4px #EADDCA, 1.5px 1.5px 2.5px 1.5px rgba(0, 0, 0, 0.5);
}</style>