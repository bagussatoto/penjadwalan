<template>
  <!-- card item start -->
  <div class="card-item-container w-full" data-cy="card-item-title">
    <div
      class="px-5 py-3 rounded-lg flex bg-white items-center justify-between shadow-md"
    >
      <div class="item-name text-xl text-slate-600">{{ nama_mk }}</div>
      <div class="action text-xl">
        <button
          class="p-2 text-slate-400 hover:text-slate-500"
          title="edit jadwal"
          data-cy="card-item-edit"
          @click="showEditModalBox"
        >
          <font-awesome-icon icon="fa-solid fa-pen-to-square" />
        </button>
        <button
          class="p-2 text-slate-400 hover:text-red-500"
          title="hapus jadwal"
          data-cy="card-item-delete"
          @click="showDeleteModalBox"
        >
          <font-awesome-icon icon="fa-solid fa-trash" />
        </button>
      </div>
    </div>

    <DetailModalBoxDelete
      :state_event="isShowDeleteModalBox"
      :hide_event="hideDeleteModalBox"
      :id_schedule="id_mk"
    />
    <DetailModalBoxEdit
      :state_event="isShowEditModalBox"
      :hide_event="hideEditModalBox"
      :id_schedule="id_mk"
      :title_schedule="nama_mk"
    />
  </div>
  <!-- card item end -->
</template>

<script>
import DetailModalBoxDelete from "./DetailModalBoxDelete.vue";
import DetailModalBoxEdit from "./DetailModalBoxEdit.vue";

export default {
  props: ["nama_mk", "show_edit_event", "id_mk"],
  data() {
    return {
      isShowDeleteModalBox: false,
      isShowEditModalBox: false,
    };
  },
  methods: {
    showDeleteModalBox() {
      this.isShowDeleteModalBox = true;
    },
    hideDeleteModalBox() {
      this.isShowDeleteModalBox = false;
    },
    showEditModalBox() {
      this.isShowEditModalBox = true;
    },
    hideEditModalBox() {
      this.isShowEditModalBox = false;
    },
  },
  components: { DetailModalBoxDelete, DetailModalBoxEdit },
};
</script>
