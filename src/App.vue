<template>
  <table class="w-screen">
    <thead class="bg-blue-900 text-white h-16">
      <tr>
        <th>Estado</th>
        <th>Nombre</th>
        <th>Precio</th>
        <th>Opciones</th>
      </tr>
    </thead>
    <tbody class="text-center">
      <tr v-for="(product, index) in products" :key="index">
        <td>
          <input v-model="product.status" type="checkbox" id="cbox2" />
          <label for="cbox2"></label>
        </td>
        <td v-if="index == position">
          <input
            v-model="product.name"
            class="border-b border-blue-800 focus:outline-none text-center"
            type="text"
            id="name"
            name="name"
            required
          />
        </td>
        <td v-else>
          {{ product.name }}
        </td>

        <td v-if="index == position">
          <input
            v-model="product.price"
            class="border-b border-blue-800 focus:outline-none text-center"
            type="number"
            id="name"
            name="name"
            required
          />
        </td>

        <td v-else>$ {{ product.price }}</td>
        <td>
          <button>
            <Save
              v-if="position == index"
              @click="save()"
              class="h-7 text-blue-700 rounded-lg"
            />
          </button>
          <button v-if="position != index" @click="edit(index)">
            <Pencil class="h-7 text-green-700 rounded-lg" />
          </button>

          <button @click="delet(index)">
            <Trash class="h-7 text-red-700 rounded-lg" />
          </button>
        </td>
      </tr>
    </tbody>
  </table>
  <button
    @click="add()"
    class="bg-blue-700 hover:bg-blue-800 rounded-full fixed bottom-2 right-2"
  >
    <PlusSm class="h-16 text-white" />
  </button>
</template>

<script>
import PlusSm from "@/components/icons/PlusSm.vue";
import Pencil from "@/components/icons/Pencil.vue";
import Save from "@/components/icons/Save.vue";
import Trash from "@/components/icons/Trash.vue";
export default {
  components: {
    PlusSm,
    Pencil,
    Save,
    Trash,
  },
  data() {
    return {
      position: null,
      products: [
        { name: "Harina", price: " 1.90", status: false },
        { name: "Harina", price: "1.90", status: true },
        { name: "va a quedae", price: " 0", status: true },
      ],
    };
  },
  methods: {
    add() {
      this.products = [
        { name: "", price: "", status: false },
        ...this.products,
      ];
      this.position = 0;
    },
    edit(index) {
      this.position = index;
    },

    save() {
      this.position = null;
    },

    delet(index) {
      this.products = [
        ...this.products.slice(0, index),
        ...this.products.slice(index + 1),
      ];
    },
  },
};
</script>