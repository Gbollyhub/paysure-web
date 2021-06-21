<template>
  <div>
            <Loader v-show="loader"/>
    <div class="login-block">
      <div class="row">
        <router-link to="/">
          <img class="img-abs" src="../../assets/images/paysure_White.png" />
        </router-link>

        <div
          id="carouselExampleIndicators"
          class="carousel slide col-lg-4"
          data-ride="carousel"
        >
          <ol class="carousel-indicators">
            <li
              data-target="#carouselExampleIndicators"
              data-slide-to="0"
              class="active"
            ></li>
            <li data-target="#carouselExampleIndicators" data-slide-to="1"></li>
            <li data-target="#carouselExampleIndicators" data-slide-to="2"></li>
          </ol>
          <div class="carousel-inner">
            <div class="carousel-item active">
              <img
                class="d-block w-100"
                src="../../assets/images/caro1.png"
                alt="First slide"
              />
            </div>
            <div class="carousel-item">
              <img
                class="d-block w-100"
                src="../../assets/images/caro1.png"
                alt="Second slide"
              />
            </div>
            <div class="carousel-item">
              <img
                class="d-block w-100"
                src="../../assets/images/caro1.png"
                alt="Third slide"
              />
            </div>
          </div>
        </div>
        <div class="col-lg-8" style="overflow:scroll">
          <div class="container resize">
            <form @submit.prevent="Login">
              <h1 class="title" style="font-size:35px">Get Started!</h1>
              <h4 class="mt-3 title-2">
                Let's get you started creating a new account
              </h4>
              <div class="form-row mt-3">
                <div class="col">
                  <label class="formlabel" for="formGroupExampleInput"
                    >First Name</label
                  >
                  <input
                    type="text"
                    class="form-control"
                    id="formGroupExampleInput"
                    placeholder=""
                  />
                </div>
                <div class="col">
                  <label class="formlabel" for="formGroupExampleInput"
                    >Last Name</label
                  >
                  <input
                    type="text"
                    class="form-control"
                    id="formGroupExampleInput"
                    placeholder=""
                  />
                </div>
              </div>
              <div class="form-row mt-3">
                <div class="col">
                  <label class="formlabel" for="formGroupExampleInput"
                    >Phone No</label
                  >
                  <input
                    type="text"
                    class="form-control"
                    id="formGroupExampleInput"
                    placeholder=""
                  />
                </div>
                <div class="col">
                  <label class="formlabel" for="formGroupExampleInput"
                    >Email</label
                  >
                  <input
                    type="text"
                    class="form-control"
                    id="formGroupExampleInput"
                    placeholder=""
                  />
                </div>
              </div>
              <div class="form-row mt-3">
                <div class="col">
                  <label class="formlabel" for="formGroupExampleInput"
                    >Password</label
                  >
                  <input
                    type="password"
                    class="form-control"
                    id="formGroupExampleInput"
                    placeholder=""
                  />
                </div>
                <div class="col">
                  <label class="formlabel" for="formGroupExampleInput"
                    >Confirm Password</label
                  >
                  <input
                    type="password"
                    class="form-control"
                    id="formGroupExampleInput"
                    placeholder=""
                  />
                </div>
              </div>

              <div class=" mt-3">
                <div class="form-check mt-3">
                  <input
                    class="form-check-input"
                    type="checkbox"
                    id="gridCheck"
                  />
                  <label class="form-check-label title-2" for="gridCheck">
                    Yes, I want to receive paysure's newsletter
                  </label>
                </div>
                <div class="form-check mt-3">
                  <input
                    class="form-check-input"
                    type="checkbox"
                    id="gridCheck"
                  />
                  <label class="form-check-label title-2" for="gridCheck">
                    I agree to all Paysure's
                    <span style="color:var(--primary-color)"
                      >Terms & Conditions</span
                    >
                  </label>
                </div>
              </div>

              <div class="center mt-5">
                <router-link tag="button" to="dashboard" class="btn-login">
                  Create Account
                </router-link>
              </div>
              <div class="center">
                <p class="title-2 mt-3">
                  Dont Have An Account?
                  <router-link
                    to="/login"
                    class="title-2"
                    style="color:var(--primary-color)"
                    >Sign In</router-link
                  >
                </p>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Loader from "@/components/loader.vue"
import axios from '@/plugins/axios'
export default {
  name: "signUp",
    components: {
    Loader
  },
  data(){
    return{
      loader:false,
      username:'',
      password:'',
      form:{
    "username": "",
    "password": "",
    "transactionPin": "",
    "phoneNumber": "",
    "emailAddress": "",
    "bvn": "",
    "state": "",
    "addressLine1": "",
    "lga": "",
    "city": ""
}

    }
  },
  methods:{
    async sendRequest(){
         try {
        const response = await axios().post(process.env.BASE_URL  + 'users/register/user',form)
        if(response.data.responseCode === 0){
          this.loader = false;
            this.$toast.open({
        message: "Registration Successful",
        type: "success",
        duration: 5000,
        dismissible: true,
        position:'top-right',
    });
        }
        else{
          this.loader = false;
                 this.$toast.open({
        message: response.data.responseMessage,
        type: "error",
        duration: 5000,
        dismissible: true,
        position:'top-right',
    });
        }

      } catch (error) {
        console.log(error)
        this.loader = false;
          this.$toast.open({
        message: response.data.responseMessage,
        type: "error",
        duration: 5000,
        dismissible: true,
        position:'top-right',
    });
      }
    }
  }
};
</script>

<style scoped>
.login-block {
  height: auto;
  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  max-width: 100%;

  background: var(--body-color);
}
.title {
  color: var(--primary-color);
}
.title-2 {
  font-size: var(--smaller-font-size);
  color: var(--text-color);
}

.carousel-item,
.carousel-inner,
.carousel-inner img {
  height: 100%;
  width: auto;
}
.carousel-item {
  text-align: center;
}
.carousel {
  height: 720px;
}

.carousel-inner img {
  width: 100%;
  height: auto;
}
/* padding: 50px 0;
}

.carousel-height{
  height: auto;
}


.carousel-inner {
	border-radius: 0 10px 10px 0;
}

.carousel-caption {
	text-align: left;
	left: 5%;
}*/

.resize {
  padding: 4rem;
}
.carousel-indicators {
  position: absolute;
  right: 0;

  left: 0;
  bottom: 50px;
  z-index: 15;

  margin-right: auto;
  margin-left: auto;
  list-style: none;
}
.pull-right {
  display: flex;
  justify-content: space-between;
}
.formlabel {
  font-weight: var(--font-semi-bold);
  font-size: var(--smaller-font-size);
}
@media screen and (max-width: 992px) {
  .login-block {
    overflow: auto;
  }
  .carousel-indicators {
    bottom: 0;
  }
  .carousel {
    display: none;
  }
}

.btn-login {
  padding: 10px 10px;
  background-color: var(--primary-color);
  color: var(--white-color);
  border-radius: 4px;
  width: 400px;
  height: 52px;

  cursor: pointer;
  -moz-transition: box-shadow 1s;
  -o-transition: box-shadow 1s;
  -webkit-transition: box-shadow 1s;
  transition: box-shadow 1s;
}

.banner-sec {
  display: flex;
  align-items: center;
  /* justify-content: center; */
}
.img-abs {
  position: absolute;
  max-width: 100% !important;
  z-index: 1;
  height: 30px !important;
  margin: 20px;
  top: 0px;
}
.carousel-indicators li {
  width: 30px !important;
  height: 10px !important;
  border-radius: 50% !important;
}
.carousel-indicators {
  width: 40px !important;
  height: 15px;
  border-radius: 50% !important;
}
.carousel-inner {
  background-image: url(../../assets/images/Overlay.svg);
}
</style>
