<template>
  <div class="background">
    <h1>Menu</h1>
    <div class="board">
      <h1>Drinks</h1>
      <div class="menuCard">
        <OrderCard
          v-for="Menu in Menus"
          :key="Menu.id"
          v-bind="Menu"
          @TakeOrder="TakingOrder"
        />
      </div>
    </div>
    <div class="detail">
      <!-- Nama -->
      <b-form-group
        id="input-group-1"
        label="Nama Pemesan:"
        label-for="Nama"
        description="Tulis Nama Anda"
      >
        <b-form-input
          id="Nama"
          v-model="Form.Nama"
          type="text"
          placeholder="Tulis Nama Anda"
          autocomplete="off"
          required
        ></b-form-input>
      </b-form-group>
      <!-- No Hp -->
      <b-form-group
        id="input-group-2"
        label="No Hp:"
        label-for="NoHP"
        description="Tulis No Hp Anda"
      >
        <b-form-input
          id="NoHP"
          v-model="Form.NoHP"
          type="text"
          placeholder="Tulis No Hp Anda"
          autocomplete="off"
          required
        ></b-form-input>
      </b-form-group>
      <!-- Alamat -->
      <b-form-group
        id="input-group-3"
        label="Alamat:"
        label-for="Alamat"
        description="Tulis Alamat Anda"
      >
        <b-form-input
          id="Alamat"
          v-model="Form.Alamat"
          type="text"
          placeholder="Tulis Alamat Anda"
          autocomplete="off"
          required
        ></b-form-input>
      </b-form-group>
      <!-- Diantar Jam -->
      <b-form-group
        id="input-group-4"
        label="Diantar Jam:"
        label-for="DiantarJam"
        description="Tulis Diantar Jam Berapa"
      >
        <b-form-input
          id="DiantarJam"
          v-model="Form.DiantarJam"
          type="text"
          placeholder="Tulis Diantar Jam Berapa"
          autocomplete="off"
          required
        ></b-form-input>
      </b-form-group>
      <!-- Diantar Dari -->
      <b-form-group
        id="input-group-5"
        label="Diantar Dari:"
        label-for="DiantarDari"
        description="Tulis Diantar Dari Mana"
      >
        <b-form-input
          id="DiantarDari"
          v-model="Form.DiantarDari"
          type="text"
          placeholder="Tulis Diantar Dari Mana"
          autocomplete="off"
          required
        ></b-form-input>
      </b-form-group>
    </div>
    <div class="wabutton">
      <b-button @click="OrderMe">Whatsapp my Order!!</b-button>
    </div>
  </div>
</template>

<script>
import OrderCard from "./OrderCard";
export default {
  name: "OrderForm",
  components: {
    OrderCard,
  },
  data() {
    return {
      Menus: [
        {
          id: 0,
          Name: "Coca Cola",
          Url:
            "https://images2.minutemediacdn.com/image/upload/c_crop,h_843,w_1500,x_0,y_70/f_auto,q_auto,w_1100/v1555172501/shape/mentalfloss/iStock-487787108.jpg",
          Price: 5000,
        },
        {
          id: 1,
          Name: "Sprite",
          Url: "https://lasolas.ca/wp-content/uploads/2020/07/sprite.jpg",
          Price: 6000,
        },
        {
          id: 2,
          Name: "Fanta",
          Url:
            "https://www.static-src.com/wcsstore/Indraprastha/images/catalog/full/MTA-2168432/fanta_fanta-strawberry-minuman-bersoda--390-ml-_full05.jpg",
          Price: 7000,
        },
      ],
      Order: [
        ["Coca Cola", 0, 5000],
        ["Sprite", 0, 6000],
        ["Fanta", 0, 7000],
      ],
      Form: {
        Nama: "",
        NoHP: "",
        Alamat: "",
        DiantarJam: "",
        DiantarDari: "",
        Total: 0,
      },
    };
  },
  methods: {
    OrderMe() {
      const datas = [];
      let Total = 0;
      this.Order.map((x) => {
        if (x[1] !== 0) {
          console.log(x);
          datas.push(x);
        }
      });
      datas.map((x) => {
        Total += Number(x[1] * x[2]);
      });
      let pesanan = "";
      datas.map((x) => {
        pesanan += `   ${x[0]} - ${x[1]} - ${Number(x[1] * x[2])}`;
        pesanan += `\r\n`;
      });
      let message = "";
      message += "Form Bulk Order Anti Lapar Club";
      message += "\r\n";
      message += "\r\n";
      message += `Nama: ${this.Form.Nama}`;
      message += "\r\n";
      message += `No Hp: ${this.Form.NoHP}`;
      message += "\r\n";
      message += `Alamat: ${this.Form.Alamat}`;
      message += "\r\n";
      message += `Diantar Jam ${this.Form.DiantarJam}`;
      message += "\r\n";
      message += `Diantar Dari: ${this.Form.DiantarDari}`;
      message += "\r\n";
      message += `Pesanan:`;
      message += "\r\n";
      message += pesanan;
      message += "\r\n";
      message += `total: ${Total}`;
      message += "\r\n";
      message += "\r\n";
      message += `Mohon Melakukan Pembayaran dengan Transfer Ke:\r\nNo rek BCA 1234567890 A.N Anti Lapar Club`;
      message += "\r\n";
      const encode = encodeURIComponent(message);
      const phone = process.env.VUE_APP_PHONE
      window.open(`http://wa.me/${phone}?text=${encode}`, "_blank");
      
    },
    TakingOrder(value) {
      switch (value.Name) {
        case "Coca Cola":
          this.Order[0][1] = Number(value.Quantity);
          break;
        case "Sprite":
          this.Order[1][1] = Number(value.Quantity);
          break;
        case "Fanta":
          this.Order[2][1] = Number(value.Quantity);
          break;
        default:
          break;
      }
    },
  },
};
</script>

<style>
.board {
  background-color: orange;
  height: 60vh;
  width: 80vw;
  margin-left: 10vw;
  margin-right: 10vw;
  display: flex;
  flex-direction: column;
  overflow: auto;
  padding-left: 2vw;
  padding-right: 2vw;
}
.wabutton {
  background-color: red;
  margin-left: 10vw;
  margin-right: 10vw;
  width: 80vw;
}
.menuCard {
  height: 58vh;
  width: 60;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  margin-right: 1vw;
  margin-left: 1vw;
  padding-left: 1vw;
  padding-right: 1vw;
  flex-wrap: wrap;
}
.detail {
  width: 80vw;
  margin-left: 10vw;
  margin-right: 10vw;
}
</style>
