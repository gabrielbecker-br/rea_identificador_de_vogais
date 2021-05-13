<template>
  <div>
    <h1>Identificador de Vogais</h1>
    <h2>Escreva uma palavra e verifique as vogais</h2>
    <br />

    <div>
      <label>Digite uma palavra</label>
      <br />
      <input
        id="input_palavra"
        type="text"
        v-on:keyup="contarLetras(), (palavra = $event.target.value)"
        placeholder="palavra"
      />

      <button v-on:click="reiniciar()">
        Reiniciar
      </button>
    </div>
    <p>Caracteres: {{ caracteres }}</p>
    <br />
    <div>
      <label>Contador das vogais:</label>
      <br />
      <p>Palavra verificada: {{ palavra }}</p>
      <ul>
        <li v-for="valor in this.vogais" v-bind:key="valor">
          {{ valor.letra }} -> {{ valor.contador }} ocorrências
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.css';
import 'font-awesome/css/font-awesome.css';

export default {
  name: 'App',
  data: function() {
    return {
      caracteres: 0,
      palavra: '',
      vogais: [
        {
          letra: 'A',
          contador: 0,
          teste: 0,
        },
        {
          letra: 'E',
          contador: 0,
          teste: 0,
        },
        {
          letra: 'I',
          contador: 0,
          teste: 0,
        },
        {
          letra: 'O',
          contador: 0,
          teste: 0,
        },
        {
          letra: 'U',
          contador: 0,
          teste: 0,
        },
      ],
    };
  },
  methods: {
    contarLetras() {
      let palavraDigitada = document
        .getElementById('input_palavra')
        .value.toLowerCase()
        .normalize('NFD')
        .replace(/[\u0300-\u036f]/g, '');

      this.caracteres = palavraDigitada.length;

      this.vogais[0].contador = (palavraDigitada.match(/a/g) || []).length;
      this.vogais[1].contador = (palavraDigitada.match(/e/g) || []).length;
      this.vogais[2].contador = (palavraDigitada.match(/i/g) || []).length;
      this.vogais[3].contador = (palavraDigitada.match(/o/g) || []).length;
      this.vogais[4].contador = (palavraDigitada.match(/u/g) || []).length;
    },
    reiniciar() {
      for (let i = 0; i < 5; i++) {
        this.vogais[i].contador = 0;
      }

      this.caracteres = 0;
      document.getElementById('input_palavra').value = '';
    },
  },
};
</script>

<style></style>
