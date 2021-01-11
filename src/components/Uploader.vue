<template>
  <div
    style="
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
    "
  >
    <div class="avatar" id="avatar" ref="avatar" :style="style">
      <i
        class="material-icons avatar-icon"
        v-if="style.backgroundImage == 'none'"
        >face</i
      >
      <div
        class="avatar-button--container"
        :style="{ right: style.backgroundImage == 'none' ? '10px' : '0px' }"
      >
        <button
          v-if="style.backgroundImage == 'none'"
          class="avatar-button"
          @click="open"
        >
          <i class="material-icons icon">edit</i>
        </button>
        <button
          v-if="style.backgroundImage != 'none'"
          class="avatar-button--secondary"
          @click="style.backgroundImage = 'none'"
        >
          <i class="material-icons icon">delete</i>
        </button>
        <button
          v-if="style.backgroundImage !== 'none'"
          class="avatar-button--secondary"
          @click="uploadImage"
        >
          <div class="spinner" v-if="uploading">
            <div class="double-bounce1"></div>
            <div class="double-bounce2"></div>
          </div>
          <i class="material-icons icon" v-if="!uploading">upload</i>
        </button>
      </div>
    </div>
    <transition
      appear
      enter-active-class="animated fadeInUp"
      leave-active-class="animated fadeOutRight"
      :duration="{ enter: 1000, leave: 1000 }"
    >
      <div class="uploader-notifications" v-if="notification.show">
        {{ notification.message }}
      </div>
    </transition>
    <input
      type="file"
      v-on:change="previewFiles"
      accept="image/*,.pdf"
      name="avatar"
      id="uploader"
      v-show="false"
    />
  </div>
</template>
<script>
export default {
  data() {
    return {
      uploading: false,
      file: null,
      style: {
        backgroundColor: "steelblue",
        backgroundImage: "none",
      },
      notification: {
        show: false,
        message: "Success!",
      },
    };
  },
  methods: {
    open() {
      document.getElementById("uploader").click();
    },
    previewFiles(event) {
      const img = event.target.files[0];
      let reader = new FileReader();
      reader.onload = (event) => {
        this.style.backgroundImage = `url(${event.target.result})`;
      };
      if (img) {
        reader.readAsDataURL(img);
        this.file = img;
      }
    },
    uploadImage() {
      this.uploading = true;
      setTimeout(() => {
        this.uploading = false;
        this.showNotification();
      }, 1800);
    },
    showNotification() {
      this.notification.show = true;
      setTimeout(() => {
        this.notification.show = false;
      }, 2500);
    },
  },
};
</script>
<style lang="scss" scoped>
.uploader-notifications {
  margin-top: 3%;
  padding: 3% 7%;
  font-size: 1.3em;
  color: limegreen;
}
.avatar {
  width: 200px;
  height: 200px;
  border-radius: 50%;
  position: relative;
  background-color: "#90e0ef";
  display: flex;
  justify-content: center;
  align-items: center;
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
  .avatar-icon {
    color: #fefefe;
    font-size: 7em;
    opacity: 0.9;
  }
  .avatar-button--container {
    position: absolute;
    bottom: 0;
    display: flex;
    flex-direction: row;
    .avatar-button {
      border-radius: 50%;
      width: 40px;
      height: 40px;
      display: flex;
      justify-content: center;
      align-items: center;
      border: none !important;
      outline: none !important;
      cursor: pointer;
      &:hover {
        background: #0077b6;
        color: #fff !important;
        transition: all 0.3s;
        .icon {
          color: white;
        }
      }
      .icon {
        color: grey;
      }
    }
    .avatar-button--secondary {
      border-radius: 50%;
      width: 40px;
      height: 40px;
      margin-left: 5px;
      display: flex;
      justify-content: center;
      align-items: center;
      border: none !important;
      outline: none !important;
      cursor: pointer;
      &:hover {
        background: #0077b6;
        color: #fff !important;
        transition: all 0.3s;
        .icon {
          color: white;
        }
      }
      .icon {
        color: grey;
      }
    }
  }
}
// Spinner
.spinner {
  width: 15px;
  height: 15px;

  position: relative;
  margin: 100px auto;
}

.double-bounce1,
.double-bounce2 {
  width: 100%;
  height: 100%;
  border-radius: 50%;
  background-color: #333;
  opacity: 0.6;
  position: absolute;
  top: 0;
  left: 0;

  -webkit-animation: sk-bounce 2s infinite ease-in-out;
  animation: sk-bounce 2s infinite ease-in-out;
}

.double-bounce2 {
  -webkit-animation-delay: -1s;
  animation-delay: -1s;
}

@-webkit-keyframes sk-bounce {
  0%,
  100% {
    -webkit-transform: scale(0);
  }
  50% {
    -webkit-transform: scale(1);
  }
}

@keyframes sk-bounce {
  0%,
  100% {
    transform: scale(0);
    -webkit-transform: scale(0);
  }
  50% {
    transform: scale(1);
    -webkit-transform: scale(1);
  }
}
</style>