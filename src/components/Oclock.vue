<template>
  <main class="background">
    <Transition>
      <header v-if="state">
        <div>
          <span>{{ hours }}</span>
        </div>
        <div><span>:</span></div>
        <div>
          <span>{{ minutes }}</span>
        </div>
        <div><span>:</span></div>
        <div>
          <span>{{ seconds }}</span>
        </div>
      </header>
    </Transition>
  </main>
  <Loading v-if="!state" />
</template>

<script setup lang="ts">
import { ref, watchEffect } from "vue";
import Loading from "@/components/Loading.vue";

let hours = ref<string>("");
let minutes = ref<string>("");
let seconds = ref<string>("");

const delay = 1000;

setInterval(() => {
  const date = new Date();

  hours.value = String(
    date.getHours() < 10 ? "0" + date.getHours() : date.getHours()
  );
  minutes.value = String(
    date.getMinutes() < 10 ? "0" + date.getMinutes() : date.getMinutes()
  );
  seconds.value = String(
    date.getSeconds() < 10 ? "0" + date.getSeconds() : date.getSeconds()
  );
}, delay);

let state = ref<boolean>(false);

watchEffect(() => {
  if (hours.value && minutes.value && seconds.value) {
    state.value = true;
  }
});
</script>

<style scoped>
.background {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: rgb(20, 20, 20);
  padding: 0 2%;

  header {
    display: flex;
    justify-content: center;
    align-items: center;

    div {
      span {
        color: rgb(243, 243, 243);
        font-size: 200px;
      }
    }

    div:nth-of-type(1),
    div:nth-of-type(3),
    div:nth-of-type(5) {
      text-align: center;
      width: 210px;
    }
  }
}

@media screen and (max-width: 1024px) {
  .background {
    header {
      div {
        span {
          font-size: 150px;
        }
      }

      div:nth-of-type(1),
      div:nth-of-type(3),
      div:nth-of-type(5) {
        text-align: center;
        width: 160px;
      }
    }
  }
}

@media screen and (max-width: 768px) {
  .background {
    header {
      div {
        span {
          font-size: 100px;
        }
      }

      div:nth-of-type(1),
      div:nth-of-type(3),
      div:nth-of-type(5) {
        text-align: center;
        width: 110px;
      }
    }
  }
}

@media screen and (max-width: 520px) {
  .background {
    header {
      div {
        span {
          font-size: 60px;
        }
      }

      div:nth-of-type(1),
      div:nth-of-type(3),
      div:nth-of-type(5) {
        text-align: center;
        width: 70px;
      }
    }
  }
}

.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>
