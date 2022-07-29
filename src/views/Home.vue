<template>
  <div class="home">
    <section class="ctr-main">
      <div>
        <h3>Personal information</h3>
        <h6>
          This information will be displayedly so be careful what you share.
        </h6>
      </div>

      <section>
        <div class="ctr-input">
          <label for="">Full Name</label>
          <input type="text" placeholder="Your Name" />
        </div>
        <div class="ctr-input">
          <label for="">Email address</label>
          <input type="email" placeholder="yourmail@mail.com" />
        </div>
        <div class="ctr-input">
          <label for="">Date of Birth</label>
          <input type="text" placeholder="dd/mm/yy" />
        </div>
        <div class="ctr-input">
          <label for="">Address</label>
          <input type="text" placeholder="Street Address" />
        </div>
        <div class="ctr-input">
          <label for="">Phone Number</label>
          <input type="text" placeholder="e.g 813 2811 2993" />
        </div>
        <div class="ctr-input">
          <label for="">Password</label>
          <input type="password" placeholder="**********" />
          <h6>
            Minimum of 6 characters, with upper & lower case, a number and a
            symbol.
          </h6>
        </div>
      </section>

      <hr />

      <section class="button-list">
        <div>
          <button class="btn-1">Cancel</button>
          <button class="btn-2">Submit</button>
        </div>
        <button class="btn-3" @click="getRandomuser">Auto Generate</button>
      </section>

      <section class="clear-list">
        <hr />
        <h6 class="clear-text" @click="dataUser = []">Clear All List User</h6>
        <hr />
      </section>

      <section>
        <div class="search">
          <div class="inset-transparent">
            <img src="/img/icons/magnify.png" alt="" />
          </div>
          <input type="text" placeholder="Search Anything" />
        </div>
      </section>

      <section class="user-ctr">
        <div class="card-user" v-for="(user, uKey) in dataUser" :key="uKey">
          <img class="icon" :src="user.picture.large" alt="" />
          <h6 class="text-center">Hi, My {{ user.tab }} is</h6>
          <h3 class="text-center">
            {{ displayText(user) }}
          </h3>
          <div class="button-icon">
            <div
              :class="[user.tab === 'name' && 'hover']"
              @mouseenter="user.tab = 'name'"
              @mouseleave="user.tab = 'name'"
            >
              <img src="/img/icons/user.png" alt="" />
            </div>
            <div
              :class="[user.tab === 'email address' && 'hover']"
              @mouseenter="user.tab = 'email address'"
              @mouseleave="user.tab = 'name'"
            >
              <img src="/img/icons/user.png" alt="" />
            </div>
            <div
              :class="[user.tab === 'birthday' && 'hover']"
              @mouseenter="user.tab = 'birthday'"
              @mouseleave="user.tab = 'name'"
            >
              <img src="/img/icons/user.png" alt="" />
            </div>
            <div
              :class="[user.tab === 'address' && 'hover']"
              @mouseenter="user.tab = 'address'"
              @mouseleave="user.tab = 'name'"
            >
              <img src="/img/icons/user.png" alt="" />
            </div>
            <div
              :class="[user.tab === 'phone number' && 'hover']"
              @mouseenter="user.tab = 'phone number'"
              @mouseleave="user.tab = 'name'"
            >
              <img src="/img/icons/user.png" alt="" />
            </div>
            <div
              :class="[user.tab === 'password' && 'hover']"
              @mouseenter="user.tab = 'password'"
              @mouseleave="user.tab = 'name'"
            >
              <img src="/img/icons/user.png" alt="" />
            </div>
          </div>
        </div>
      </section>
    </section>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from "vue";
import axios from "axios";
import moment from "moment";

export default defineComponent({
  setup() {
    const dataUser = ref();

    onMounted(() => {
      dataUser.value = [];
    });

    const displayText = (data: any) => {
      switch (data.tab) {
        case "name":
          return data.name.first + " " + data.name.last;

        case "email address":
          return data.email;

        case "birthday":
          return moment(data.dob.date).format("D/M/YYYY");

        case "address":
          return data.location.city + " " + data.location.state;

        case "phone number":
          return data.phone;

        case "password":
          return data.password ?? "";

        default:
          break;
      }
    };

    const getRandomuser = () => {
      axios
        .get("https://randomuser.me/api/?results=10")
        .then((res: any) => {
          dataUser.value = res.data.results.map((data: any) => {
            return {
              ...data,
              tab: "name",
            };
          });
        })
        .catch((err) => {
          console.log(err);
        });
    };

    return {
      dataUser,
      displayText,
      getRandomuser,
    };
  },
});
</script>

<style scoped>
body {
  font-family: "Inter";
  font-style: normal;
}
h3 {
  margin-bottom: 5px;
  font-size: 18px;
}
h6 {
  margin-top: 5px;
  color: #6b7280;
  font-size: 14px;
  font-weight: normal;
}
.ctr-input {
  margin-bottom: 10px;
}
label {
  font-size: 14px;
  color: #374151;
  display: block;
  margin-bottom: 5px;
}
input {
  border: 1px solid #d1d5db;
  box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 6px;
  width: 95%;
  height: 20px;
  padding: 9px 13px;
}
.ctr-main {
  width: 700px;
  margin: auto;
}
hr {
  border-color: #e5e7eb;
  margin: 20px 0;
}
button {
  padding: 9px 17px;
  border-radius: 6px;
  cursor: pointer;
}
.btn-1 {
  background: #ffffff;
  color: #374151;
  border: 1px solid #d1d5db;
  box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.05);
  margin-right: 5px;
}
.btn-2 {
  background: #4f46e5;
  color: #ffffff;
  border: 1px solid #d1d5db;
  box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.05);
  margin-left: 5px;
}
.clear-list {
  display: flex;
  justify-content: space-between;
  align-items: center;
  cursor: pointer;
  margin: 50px 0;
}
.clear-list > hr {
  width: 35%;
}
.clear-text {
  margin: 0 auto;
}
.button-list {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.btn-3 {
  background: #e0e7ff;
  color: #4338ca;
  border: 1px solid #d1d5db;
  box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.05);
}
.search {
  position: relative;
}
.search > input {
  width: 35%;
  padding-left: 40px;
}
.inset-transparent {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  left: 15px;
}
.inset-transparent > img,
.button-icon img {
  width: 20px;
  height: 20px;
}
.card-user {
  box-shadow: 0px 1px 3px rgba(0, 0, 0, 0.1), 0px 1px 2px rgba(0, 0, 0, 0.06);
  border-radius: 8px;
  width: 250px;
  height: 250px;
  margin: 30px 10px;
  padding: 20px;
  position: relative;
}
.card-user > h3,
.card-user > h6 {
  margin: 0;
}
.icon {
  background: linear-gradient(315deg, #4fa0ff 0%, #83f8ff 100%);
  height: 150px;
  border-radius: 50%;
  margin-bottom: 10px;
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 50%;
}
.text-center {
  text-align: center;
}
.user-ctr {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
.button-icon {
  display: flex;
  align-items: center;
  justify-content: space-between;
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  border-top: 1px solid #e5e7eb;
}
.button-icon div {
  width: 100%;
  padding: 10px;
  text-align: center;
  border-right: 1px solid #e5e7eb;
  cursor: pointer;
}
.button-icon div.hover {
  border-top: 2px solid #e64b41;
}
</style>
