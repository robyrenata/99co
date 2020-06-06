<template>
  <div class="row text-center" id="align-mid">
    <div class="col-2 p-0 m-0">
      <button class="circle text-center" @click="pageButton('prev')" v-if="page != 0">
        <img :src="require('../../assets/icon/arrow-left.svg')" alt="arrow_left" />
      </button>
    </div>
    <div class="col-8" v-if="filterdProducts.length">
      <transition name="flip" enter-active-class="roll-in-blurred-top">
        <div class="card" v-for="(prd) in filterdProducts" :key="prd.id">
          <div class="card-header">
            <img :src="prd.productImage" />
          </div>

          <div class="card-body pl-2 pr-2">
            <div class="row" id="align-mid">
              <div class="col-10 pt-0 pb-0 text-left">
                <span class="badge" v-if="prd.type ==='sell'">Dijual</span>
                <span class="badge" v-if="prd.type ==='rent'">Disewakan</span>
                <span class="chip ml-2" v-if="prd.negotiable">Nego</span>
              </div>
              <div class="col pt-0 pb-0 text-right">
                <span class="like">
                  <img :src="require('../../assets/icon/love.svg')" alt="like" />
                </span>
              </div>
            </div>
            <div class="row" id="align-mid">
              <div class="col-xs-12 col-sm-12 col-md-12 col-lg-4 pt-0 pb-0 p0 text-left">
                <span class="price">Rp. {{prd.price}} jt</span>
              </div>
              <div class="col-xs-12 col-sm-12 col-md-12 col-lg-8 pt-0 pb-0 text-left">
                <span class="tenor">Cicilan Rp {{prd.tenor}}jt/bln</span>
              </div>
            </div>
            <div class="row">
              <div class="col-xs-6 col-sm-6 col-md-6 col-lg-3 specs pt-0 pb-0" id="align-mid">
                <span class="ico">
                  <img :src="require('../../assets/icon/bedroom.svg')" alt="bedroom" />
                </span>
                <span class="spec">{{prd.totalBedroom}} K.Tidur</span>
              </div>
              <div class="col-xs-6 col-sm-6 col-md-6 col-lg-3 specs pt-0 pb-0" id="align-mid">
                <span class="ico">
                  <img :src="require('../../assets/icon/bathroom.svg')" alt="bathroom" />
                </span>
                <span class="spec">{{prd.totalBathroom}} K.Mandi</span>
              </div>

              <div class="col-xs-6 col-sm-6 col-md-6 col-lg-3 specs pt-0 pb-0" id="align-mid">
                <span class="ico">
                  <img :src="require('../../assets/icon/building-space.svg')" alt="building_space" />
                </span>
                <span class="spec">{{prd.spaceBuilding}}m2</span>
              </div>

              <div class="col-xs-6 col-sm-6 col-md-6 col-lg-3 specs pt-0 pb-0" id="align-mid">
                <span class="ico">
                  <img :src="require('../../assets/icon/land-space.svg')" alt="land_space" />
                </span>
                <span class="spec">{{prd.spaceLand}}m2</span>
              </div>
            </div>

            <div class="row">
              <div class="col">
                <button class="btn" @click.stop="openModal('detail')">Lihat Detail</button>
              </div>
            </div>

            <v-dialog v-model="modal.isOpen" max-width="70%" click:outside="closeModal()">
              <div class="card">
                <div class="card-header">
                  <img v-if="modal.type !== 'map'" :src="prd.productImage" />
                  <img v-if="modal.type == 'map'" :src="prd.map" />
                </div>

                <div class="card-body pl-2 pr-2">
                  <div class="modal-wrapper-1" v-if="modal.type == 'detail'">
                    <div class="row" id="align-mid">
                      <div class="col-10 pt-0 pb-0 text-left">
                        <span class="badge" v-if="prd.type ==='sell'">Dijual</span>
                        <span class="badge" v-if="prd.type ==='rent'">Disewakan</span>
                        <span class="chip ml-2" v-if="prd.negotiable">Nego</span>
                      </div>
                      <div class="col-2 pt-0 pb-0 text-right">
                        <span class="like">
                          <img :src="require('../../assets/icon/love.svg')" alt="like" />
                        </span>
                      </div>
                    </div>
                    <div class="row" id="align-mid">
                      <div class="col-xs-12 col-sm-12 col-md-12 col-lg-4 pt-0 pb-0 p0 text-left">
                        <span class="price">Rp. {{prd.price}} jt</span>
                      </div>
                      <div class="col-xs-12 col-sm-12 col-md-12 col-lg-8 pt-0 pb-0 text-left">
                        <span class="tenor">Cicilan Rp {{prd.tenor}}jt/bln</span>
                      </div>
                    </div>
                    <div class="row">
                      <div
                        class="col-xs-6 col-sm-6 col-md-6 col-lg-3 specs pt-0 pb-0"
                        id="align-mid"
                      >
                        <span class="ico">
                          <img :src="require('../../assets/icon/bedroom.svg')" alt="bedroom" />
                        </span>
                        <span class="spec">{{prd.totalBedroom}} K.Tidur</span>
                      </div>
                      <div
                        class="col-xs-6 col-sm-6 col-md-6 col-lg-3 specs pt-0 pb-0"
                        id="align-mid"
                      >
                        <span class="ico">
                          <img :src="require('../../assets/icon/bathroom.svg')" alt="bathroom" />
                        </span>
                        <span class="spec">{{prd.totalBathroom}} K.Mandi</span>
                      </div>

                      <div
                        class="col-xs-6 col-sm-6 col-md-6 col-lg-3 specs pt-0 pb-0"
                        id="align-mid"
                      >
                        <span class="ico">
                          <img
                            :src="require('../../assets/icon/building-space.svg')"
                            alt="building_space"
                          />
                        </span>
                        <span class="spec">{{prd.spaceBuilding}}m2</span>
                      </div>

                      <div
                        class="col-xs-6 col-sm-6 col-md-6 col-lg-3 specs pt-0 pb-0"
                        id="align-mid"
                      >
                        <span class="ico">
                          <img :src="require('../../assets/icon/land-space.svg')" alt="land_space" />
                        </span>
                        <span class="spec">{{prd.spaceLand}}m2</span>
                      </div>
                    </div>
                  </div>

                  <div class="modal-wrapper-2" v-if="modal.type == 'map'">
                    <div class="container">
                      <div class="row" id="align-mid">
                        <div class="col-12">
                          <h1 class="text-bold">{{prd.addressName}}</h1>
                        </div>
                        <div class="col-12">
                          <p>{{prd.addressDetail}}</p>
                        </div>
                      </div>
                    </div>
                  </div>

                  <div class="row">
                    <div class="col">
                      <button
                        class="btn"
                        v-if="modal.type != 'map'"
                        @click.stop="modal.type = 'map'"
                      >Lihat Peta</button>
                      <button
                        class="btn"
                        v-if="modal.type == 'map'"
                        @click.stop="closeModal()"
                      >Tutup</button>
                    </div>
                  </div>
                </div>
              </div>
            </v-dialog>
          </div>
        </div>
      </transition>
    </div>
    <div class="col-2 p-0 m-0">
      <button
        class="circle text-center"
        @click="pageButton('next')"
        v-if="page != products.length -1"
      >
        <img :src="require('../../assets/icon/arrow-right.svg')" alt="arrow_right" />
      </button>
    </div>
  </div>
</template>




<script>
import Vue from "vue";

export default Vue.extend({
  name: "Product",

  data: () => ({
    page: 1,
    products: [
      {
        id: "001",
        productImage:
          "https://hips.hearstapps.com/hmg-prod.s3.amazonaws.com/images/suburban-house-royalty-free-image-1584972559.jpg",
        type: "sell",
        negotiable: false,
        price: 326,
        tenor: 2.61,
        totalBedroom: 2,
        totalBathroom: 2,
        spaceBuilding: 65,
        spaceLand: 65,
        map: require("../../assets/img/map.png"),
        addressName: "Jl. Alam Permai IV",
        addressDetail:
          "Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem."
      },
      {
        id: "002",
        productImage:
          "https://specials-images.forbesimg.com/imageserve/1026205392/960x0.jpg?fit=scale",
        type: "rent",
        negotiable: true,
        price: 220,
        tenor: 1.61,
        totalBedroom: 2,
        totalBathroom: 2,
        spaceBuilding: 35,
        spaceLand: 45,
        map: require("../../assets/img/map.png"),
        addressName: "Jl. Suka Jadi",
        addressDetail:
          "Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem."
      },
      {
        id: "003",
        productImage:
          "https://images.unsplash.com/photo-1580587771525-78b9dba3b914?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&w=1000&q=80",
        type: "sell",
        negotiable: true,
        price: 300,
        tenor: 3.61,
        totalBedroom: 4,
        totalBathroom: 2,
        spaceBuilding: 50,
        spaceLand: 50,
        map: require("../../assets/img/map.png"),
        addressName: "Jl. Alam Alam Alam IV",
        addressDetail:
          "Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem."
      }
    ],
    filterdProducts: [],
    modal: {
      isOpen: false,
      type: "detail"
    }
  }),

  created: function() {
    this.filterdProducts.push(this.products[this.page]);
  },

  methods: {
    openModal: function(type) {
      console.log("show modal?", type);
      this.modal.isOpen = true;
    },
    closeModal: function() {
      this.modal.isOpen = false;
      this.modal.type = "detail";
    },
    pageButton: function(type) {
      console.log("type", type);
      console.log("page", this.page);
      console.log("products", this.products);
      console.log("product", this.productSelected);

      if (type == "prev") {
        if (this.page !== 0) {
          this.page--;
          this.updateArray(this.page);
          console.log("page", this.page);
        }
      } else if (type == "next") {
        if (this.page !== this.products.length - 1) {
          this.page++;
          this.updateArray(this.page);
          console.log("page", this.page);
        }
      }
    },
    updateArray: function(i) {
      this.filterdProducts = [this.products[i]];
      console.log("fil id", this.filterdProducts);
    }
  }
});
</script>

<style lang="scss">
.circle {
  background: white;
  height: 40px;
  width: 40px;
  border-radius: 50%;
  display: inline-block;
  padding-top: 0.5em;
}

.card {
  border-radius: 10px;
  width: auto;
  height: auto;
  background-color: white;

  .card-header {
    img {
      width: 100%;
      height: 250px;
      max-height: 250px;
      padding: 0.5em;
      border-top-left-radius: 20px;
      border-top-right-radius: 20px;
      object-fit: cover;
    }
  }
}

.badge {
  background-color: lightgrey;
  color: black;
  text-align: center;
  padding: 0 10px 0 10px;
  font-weight: bold;
  font-size: 10pt;
}

.chip {
  background-color: seagreen;
  color: white;
  border-radius: 50px;
  text-align: center;
  padding: 0 10px 0 10px;
  font-weight: bold;
  font-size: 10pt;
}

.specs {
  padding-right: 0 !important;
}

.spec {
  color: black !important;
  font-size: 8pt;
  font-weight: bold;
  padding: 5px;
}

.price {
  color: black !important;
  font-weight: bold;
  font-size: 20px;
  padding: 5px;
}

.tenor {
  color: black !important;
  font-size: 10pt;
  padding: 5px;
}

.btn {
  background-color: seagreen;
  color: white;
  width: 100%;
  padding: 0.5em 0 0.5em 0;
}

.modal-wrapper-2 {
  h1,
  p {
    color: black;
  }
}

// ANIMATION
.roll-in-blurred-top {
  -webkit-animation: roll-in-blurred-top 0.6s cubic-bezier(0.23, 1, 0.32, 1)
    both;
  animation: roll-in-blurred-top 0.6s cubic-bezier(0.23, 1, 0.32, 1) both;
}

/* ----------------------------------------------
 * Generated by Animista on 2020-6-6 15:11:17
 * Licensed under FreeBSD License.
 * See http://animista.net/license for more info. 
 * w: http://animista.net, t: @cssanimista
 * ---------------------------------------------- */

/**
 * ----------------------------------------
 * animation roll-in-blurred-top
 * ----------------------------------------
 */
@-webkit-keyframes roll-in-blurred-top {
  0% {
    -webkit-transform: translateY(-800px) rotate(-720deg);
    transform: translateY(-800px) rotate(-720deg);
    -webkit-filter: blur(50px);
    filter: blur(50px);
    opacity: 0;
  }
  100% {
    -webkit-transform: translateY(0) rotate(0deg);
    transform: translateY(0) rotate(0deg);
    -webkit-filter: blur(0);
    filter: blur(0);
    opacity: 1;
  }
}
@keyframes roll-in-blurred-top {
  0% {
    -webkit-transform: translateY(-800px) rotate(-720deg);
    transform: translateY(-800px) rotate(-720deg);
    -webkit-filter: blur(50px);
    filter: blur(50px);
    opacity: 0;
  }
  100% {
    -webkit-transform: translateY(0) rotate(0deg);
    transform: translateY(0) rotate(0deg);
    -webkit-filter: blur(0);
    filter: blur(0);
    opacity: 1;
  }
}

// end of ANIMATION
</style>
