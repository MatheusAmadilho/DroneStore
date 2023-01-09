<template>
  <div id="email-table" v-if="emails">
    <div>
      <div id="email-table-heading">
        <div class="order-id">#:</div>
        <div>Cliente:</div>
      </div>
    </div>
    <div id="email-table-rows">
      <div class="email-table-row" v-for="email in emails" :key="email.id">
        <div class="order-number">{{ email.id }}</div>
        <div>{{ email.email }}</div>
      </div>
    </div>
  </div>
  <div v-else>
    <h2>Não há emails registrados!</h2>
  </div>
</template>
<script>
  export default {
    name: "Dashboard",
    data() {
      return {
        emails: null,
        email_id: null,
      }
    },
    methods: {
      async getEmails() {
        const req = await fetch('http://localhost:3000/emails')

        const data = await req.json()

        this.emails = data

      },
    },
    mounted () {
    this.getEmails()
    }
  }
</script>

<style scoped>
  #email-table {
    max-width: 1200px;
    margin: 0 auto;
  }

  #email-table-heading,
  #email-table-rows,
  .email-table-row {
    display: flex;
    flex-wrap: wrap;
  }

  #email-table-heading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
  }

  .email-table-row {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #CCC;
  }

  #email-table-heading div,
  .email-table-row div {
    width: 19%;
  }

  #email-table-heading .order-id,
  .email-table-row .order-number {
    width: 5%;
  }
  
</style>