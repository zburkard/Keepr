<template>
  <div class="modal fade pic" id="activeKeepModal" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog modal-dialog-centered modal-xl ">
      <div class="modal-content shadow all container-fluid p-0 pe-2 modalness">
        <div class="d-flex justify-content-between cols" v-if="keep">

          <div class="col-6 col1" title="Keep Image" aria-label="Keep Image">
            <img :src="keep?.img" alt="" class="img-vfx rounded-start" />
          </div>
          <div class="col-md-6 col2 d-flex justify-content-between py-4 px-5 flex-column">
            <div class="counts">
              <div class="d-flex justify-content-center">
                <div class="" title="View Count" aria-label="Keep View Count">
                  <span class="ms-2 fs-4 mdi mdi-eye">{{ keep?.views }}</span>
                </div>
                <div class="ms-3" title="Vault Count" aria-label="Keep Vault Count">
                  <span class="ms-2 mdi fs-4 mdi-alpha-k-box ">{{ keep?.kept }}</span>
                </div>
              </div>
            </div>
            <div class=" justify-content-center">
              <div class="title">
                <h4 class="d-flex justify-content-center fw-bold" title="Keep Name" aria-label="Keep Name">{{
                  keep?.name
                }}
                </h4>
              </div>
              <div class="d-flex justify-content-center desc" title="Description" aria-label="Keep description"> {{
                keep?.description
              }}</div>
            </div>
            <div class="d-flex justify-content-between">
              <div class="">
                <CreateKeepForVault />
              </div>

              <div class=" other" title="Add to a vault" aria-label="Add to a vault.">
                <div class="d-flex justify-content-between">

                  <span v-if="account.id == keep.creatorId">
                    <div class="text-white mt-3" data-bs-dismiss="modal" title="Creator name" aria-label="Creator Name">
                      <router-link :to="{ name: 'Account', params: { id: keep?.creator.id } }">
                        <img :src="keep?.creator.picture" height="50" width="50"
                          class="ms-2 rounded-circle elevation-2 hover creator" alt=""> <span class="text-dark name">{{
                            keep?.creator.name
                          }}</span>
                      </router-link>
                    </div>
                  </span>
                  <span v-else>
                    <div class="text-white userstuff mt-3" data-bs-dismiss="modal" title="Creator name"
                      aria-label="Creator Name">
                      <router-link :to="{ name: 'Profile', params: { id: keep?.creator.id } }">
                        <img :src="keep?.creator.picture" height="50" width="50"
                          class="ms-2 rounded-circle elevation-2 hover " alt="">
                        <span class="text-dark name ms-2">{{ keep?.creator.name }}</span>
                      </router-link>
                    </div>
                  </span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import { AppState } from '../AppState';
import { computed } from 'vue';
import CreateKeepForVault from "./CreateKeepForVault.vue";
import Pop from "../utils/Pop.js";
import { vaultsKeepsService } from "../services/VaultKeepsService.js";
export default {
  // props: {
  //   keep: {
  //     type: Object,
  //     required: true,
  //   }
  // },
  setup() {
    return {
      keep: computed(() => AppState.activeKeep),
      account: computed(() => AppState.account),
      vault: computed(() => AppState.activeVault),
      vaultKeeps: computed(() => AppState.vaultKeeps),

    };
  },
  components: { CreateKeepForVault }
};
</script>


<style lang="scss" scoped>
.img-vfx {
  height: 82vh;
  width: 564px;
  object-fit: cover;
}

@media screen AND (max-width: 768px) {
  .cols {
    flex-direction: column;
  }

  .col2 {
    padding: 0% !important;
  }

  .img-vfx {
    border-radius: 0% !important;
    height: 82vh;
    width: 478.5px;
    object-fit: fit;
  }

  .desc {
    text-align: center;
    padding: 1rem
  }

  .title {
    margin-top: 1rem;
  }

  .counts {
    margin-top: 1rem;
  }

  .other {
    padding-top: 1rem;
    padding-bottom: 1rem;
    padding-left: 1rem;
    padding-right: 1rem;
  }

  .name {
    margin-left: 1rem
  }

}
</style>