<script>
import AcessoriosApi from "../api/acessorios";
const acessoriosApi = new AcessoriosApi();
export default {
  data() {
    return {
      acessorios: [],
      acessorio: {},
    };
  },
  async created() {
    this.acessorios = await acessoriosApi.buscarTodosOsAcessorios();
  },
  methods: {
    async salvar() {
      if (this.acessorio.id) {
        await acessoriosApi.atualizarAcessorio(this.acessorio);
      } else {
        await acessoriosApi.adicionarAcessorio(this.acessorio);
      }
      this.acessorio = {};
      this.acessorios = await acessoriosApi.buscarTodosOsAcessorios();
    },
    editar(acessorio) {
      Object.assign(this.acessorio, acessorio);
    },
    async excluir(acessorio) {
      await acessoriosApi.excluirAcessorio(acessorio.id);
      this.acessorios = await acessoriosApi.buscarTodosOsAcessorios();
    },
  },
};
</script>

<template>
  <h1>Acessorios</h1>
  <hr />
  <div class="form">
    <input
      class="inputEnviar"
      type="text"
      v-model="acessorio.descricao"
      placeholder="Nome da acessorio"
      required
    />
    <button class="btn" @click="salvar">
      <font-awesome-icon icon="fa-solid fa-floppy-disk" /> <span>Salvar</span>
    </button>
  </div>
  <hr />
  <table>
    <tr>
      <th class="cabeça">Id da Acessorio</th>
      <th class="cabeça">Nome</th>
      <th class="cabeça">Ação</th>
    </tr>
    <tr v-for="acessorio in acessorios" :key="acessorio.id">
      <td>{{ acessorio.id }}</td>
      <td>{{ acessorio.descricao }}</td>
      <td>
        <button class="btn-excluir" @click="excluir(acessorio)">
          <font-awesome-icon icon="fa-trash" /> <span>Excluir</span>
        </button>
        <button class="btn-editar" @click="editar(acessorio)">
          <font-awesome-icon icon="fa-pencil" /> <span>Editar</span>
        </button>
      </td>
    </tr>
  </table>
</template>

<style></style>
