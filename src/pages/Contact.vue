<template>
  <div class="relative isolate bg-white px-6 py-24 sm:py-32 lg:px-8">
    <div
      class="w-full fixed bg-green-100 py-3 px-2 top-16 left-0 text-green-700 flex items-center justify-center"
      v-if="success === true"
    >
      Your messag successfully recieved, Thanks
      <router-link class="underline pl-2" to="/"> Go to Home</router-link>
    </div>
    <div class="mx-auto max-w-xl lg:max-w-4xl">
      <h2 class="text-4xl font-bold tracking-tight text-gray-900">
        Having any issue
        <span class="text-primary underline">Talk with us</span>
      </h2>

      <div class="mt-16 flex flex-col gap-16 sm:gap-y-20 lg:flex-row">
        <form @submit="submitForm" class="lg:flex-auto">
          <div class="grid grid-cols-1 gap-x-8 gap-y-6 sm:grid-cols-2">
            <div>
              <label
                for="first-name"
                class="block text-sm font-semibold leading-6 text-gray-900"
                >First name</label
              >
              <div class="mt-2.5">
                <input
                  v-model="formData.firstName"
                  type="text"
                  name="first-name"
                  id="first-name"
                  autocomplete="given-name"
                  class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                />
              </div>
            </div>
            <div>
              <label
                for="last-name"
                class="block text-sm font-semibold leading-6 text-gray-900"
                >Last name</label
              >
              <div class="mt-2.5">
                <input
                  v-model="formData.lastName"
                  type="text"
                  name="last-name"
                  id="last-name"
                  autocomplete="family-name"
                  class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                />
              </div>
            </div>
            <div>
              <label
                for="budget"
                class="block text-sm font-semibold leading-6 text-gray-900"
                >Order Id</label
              >
              <div class="mt-2.5">
                <input
                  id="budget"
                  v-model="formData.orderId"
                  name="budget"
                  type="text"
                  class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                />
              </div>
            </div>
            <div>
              <label
                for="website"
                class="block text-sm font-semibold leading-6 text-gray-900"
                >Address</label
              >
              <div class="mt-2.5">
                <input
                  type="url"
                  name="website"
                  id="website"
                  autocomplete="url"
                  v-model="formData.address"
                  class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                />
              </div>
            </div>
            <div class="sm:col-span-2">
              <label
                for="message"
                class="block text-sm font-semibold leading-6 text-gray-900"
                >Message</label
              >
              <div class="mt-2.5">
                <textarea
                  id="message"
                  name="message"
                  v-model="formData.message"
                  rows="4"
                  class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                ></textarea>
              </div>
            </div>
          </div>
          <div class="mt-10">
            <button
              type="submit"
              class="block w-full rounded-md bg-primary px-3.5 py-2.5 text-center text-sm font-semibold text-white shadow-sm hover:bg-primary focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
            >
              Send Message
            </button>
          </div>
          <p class="mt-4 text-sm leading-6 text-gray-500">
            By submitting this form, I agree to the
            <a href="#" class="font-semibold text-primary"
              >privacy&nbsp;policy</a
            >.
          </p>
        </form>
        <div class="lg:mt-6 lg:w-80 lg:flex-none">
          <h1 class="text-2xl font-semibold">Our Location</h1>
          <figure class="mt-4">
            <blockquote class="text-lg font-semibold leading-8 text-gray-900">
              <p>Main Highway Slovakia Europe</p>
            </blockquote>
          </figure>
        </div>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import { useCart } from "@/pinia/cart";

export default {
  components: {},

  props: {
    addedToCart: {
      type: Array,
      required: true,
    },
  },

  data() {
    return {
      allProducts: [],
      totalPrice: 0,
      success: false,
      form: {},
      formData: {
        firstName: "",
        lastName: "",
        orderId: "",
        address: "",
        message: "",
      },
    };
  },
  methods: {
    removeFromCart(product) {
      useCart().remove(product);
    },
    submitForm(e) {
      e.preventDefault();
      this.success = true;
      this.formData = {
        firstName: "",
        lastName: "",
        orderId: "",
        address: "",
        message: "",
      };

      setTimeout(() => {
        this.success = false;
      }, 5000);
    },
  },
  mounted() {
    this.allProducts = useCart().cart;
    this.form = useCart().formData;
  },

  computed: {
    totalPrice() {
      return this.allProducts.reduce((sum, item) => {
        const price = parseFloat(item.price.replace("$", ""));
        return sum + price;
      }, 0);
    },
  },
};
</script>
