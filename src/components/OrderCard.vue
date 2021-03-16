<template>
  <div id="Card">
    <b-card no-body class="overflow-hidden" style="max-width: 540px;">
      <b-row no-gutters>
        <b-col md="6">
          <b-card-img
            :src="Url"
            alt="Image"
            class="rounded-0"
            height="250"
            width="250"
          ></b-card-img>
        </b-col>
        <b-col md="6">
          <b-card-body :title="Name">
            <b-card-text> Price: {{ Price }} </b-card-text>
            <form>
              Quantity:
              <b-form-input
                :id="`Quantity`"
                type="number"
                v-model="Quantity"
                @change="OrderMenu"
              ></b-form-input
              ><br /><br />
            </form>
          </b-card-body>
        </b-col>
      </b-row>
    </b-card>
  </div>
</template>

<script>
export default {
  name: "MenuCard",
  data() {
    return {
      Name: this.$attrs.Name,
      Url: this.$attrs.Url,
      Price: this.$attrs.Price,
      Quantity: 0,
    };
  },
  methods: {
    OrderMenu() {
      this.$emit("TakeOrder", { Name: this.Name, Quantity: this.Quantity });
    },
  },
};
</script>

<style></style>
