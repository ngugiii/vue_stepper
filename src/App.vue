<template>
  <div class="flex p-8 w-full flex-col items-center">
    <div
      class="shadow-md w-full md:w-[70%] rounded-lg flex justify-between p-4"
    >
      <template v-for="(step, index) in steps" :key="`step-${index}`">
        <div
          class="flex flex-col items-center"
          :style="{
            marginTop: index === 0 ? '0' : '8px',
            marginBottom: index === steps.length - 1 ? '0' : '8px',
          }"
        >
          <button
            @click="setCurrentStep(index)"
            class="focus:outline-none relative"
          >
            <div class="w-10 h-10 rounded-full bg-white cursor-pointer">
              <div
                v-if="index < currentStep"
                class="bg-green-500 rounded-full w-10 h-10 flex justify-center items-center z-10 relative"
              >
                <i class="fas fa-check text-white"></i>
              </div>
              <div
                v-else-if="index === currentStep"
                class="bg-blue-500 rounded-full w-10 h-10 flex justify-center items-center z-10 relative"
              >
                <i class="fas fa-spinner fa-spin text-white"></i>
              </div>
              <div
                v-else
                class="bg-gray-300 w-full rounded-full h-10 flex justify-center items-center z-10 relative"
              >
                <!-- <span class="text-gray-500">{{ index + 1 }}</span> -->
              </div>
            </div>
          </button>
          <div class="md:text-lg text-center md:w-[9rem] w-full">
            {{ step.label }}
          </div>
          <div class="text-base text-gray-500 text-center w-full">
            {{ step.description }}
          </div>
        </div>
        <div
          :class="{
            'bg-green-500': index < currentStep,
            'bg-blue-500': index === currentStep || index === currentStep - 1,
            'bg-gray-300': index !== currentStep && index !== currentStep - 1,
          }"
          v-if="index !== steps.length - 1"
          class="h-0.5 w-full mx-1 mt-[1.5rem]"
        ></div>
      </template>
    </div>
    <div class="shadow-md rounded md:p-8 p-2 mt-6 w-full md:w-[70%]">
      <div
        v-for="(step, index) in steps"
        :key="`content-${index}`"
        v-show="index === currentStep"
        class="mb-4"
      >
        {{ step.content }}
      </div>
    </div>
    <div class="w-full md:w-[70%] flex justify-end mt-4">
      <button
        @click="nextStep"
        class="px-4 py-2 bg-blue-500 text-white rounded-md shadow-md hover:bg-blue-600 focus:outline-none mr-4"
        v-if="currentStep !== steps.length - 1"
      >
        Next
      </button>
      <button
        @click="submitForm"
        v-else
        class="px-4 py-2 bg-green-500 text-white rounded-md shadow-md hover:bg-green-600 focus:outline-none"
      >
        Submit
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentStep: 0,
      steps: [
        {
          label: "User Details",
          description: "Enter User Details",
          content: "Content for Step 1",
        },
        {
          label: "Company Details",
          description: "Enter Company Details",
          content: "Content for Step 2",
        },
        {
          label: "Select Products",
          description: "Select Products",
          content: "Content for Step 2",
        },
      ],
    };
  },
  methods: {
    setCurrentStep(index) {
      this.currentStep = index;
    },
    nextStep() {
      if (this.currentStep < this.steps.length - 1) {
        this.currentStep++;
      }
    },
    submitForm() {
      console.log("Form submitted!");
    },
  },
};
</script>

<style scoped></style>
