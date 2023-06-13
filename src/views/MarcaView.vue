<script>
import CoresApi from "../api/cores";
const coresApi = new CoresApi();
export default {
  data() {
    return {
      cores: [],
      cor: {},
    };
  },
  async created() {
    this.cores = await coresApi.buscarTodasAsCores();
  },
  methods: {
    async salvar() {
      if (this.cor.id) {
        await coresApi.atualizarCor(this.cor);
      } else {
        await coresApi.adicionarCor(this.cor);
      }
      this.cor = {};
      this.cores = await coresApi.buscarTodasAsCores();
    },
    editar(cor) {
      Object.assign(this.cor, cor);
    },
    async excluir(cor) {
      await coresApi.excluirCor(cor.id);
      this.cores = await coresApi.buscarTodasAsCores();
    },
  },
};
</script>

<template>
  <h1>Cor</h1>
  <hr />
  <div class="form">
    <input
      class="inputEnviar"
      type="text"
      v-model="cor.descricao"
      placeholder="Nome da cor"
      required
    />
    <button class="btn" @click="salvar">
      <font-awesome-icon icon="fa-solid fa-floppy-disk" /> <span>Salvar</span>
    </button>
  </div>
  <hr />
  <table>
    <tr>
      <th class="cabeça">Id do Autor</th>
      <th class="cabeça">Descrição</th>
      <th class="cabeça">Ação</th>
    </tr>
    <tr v-for="cor in cores" :key="cor.id">
      <td>{{ cor.id }}</td>
      <td>{{ cor.descricao }}</td>
      <td>
        <button class="btn-excluir" @click="excluir(cor)">
          <font-awesome-icon icon="fa-trash" /> <span>Excluir</span>
        </button>
        <button class="btn-editar" @click="editar(cor)">
          <font-awesome-icon icon="fa-pencil" /> <span>Editar</span>
        </button>
      </td>
    </tr>
  </table>
</template>

<style></style>
