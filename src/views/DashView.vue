<template>
    <div class="dashboard">
      <!-- Barre de navigation -->
      <div class="sidebar">
        <div class="sidebar-header">
          <h2 class="bank-name" style="color: white;">MA BANCO FRANCÊS</h2>
        </div>
        <div class="sidebar-menu">
          <div class="sidebar-item" @click="currentSection = 'welcome'">Bem-vindo</div>
          <div class="sidebar-item" @click="currentSection = 'viewBalance'">Pagar</div>
          <div class="sidebar-item" @click="currentSection = 'withdrawBalance'">Retirar meu saldo</div>
        </div>
        <button class="logout-button"><a style="text-decoration: none; color: white;" href="/">Déconnexion</a></button>
      </div>
  
      <!-- Contenu de la section sélectionnée -->
      <div class="main-content" style="background-color: #3EABAB;">
        <div v-if="currentSection === 'welcome'">
          <h2>BEM-VINDO ARNALDO PAULO WOBETO</h2>
          <p>{{ welcomeMessage }}</p>
          <img src="/public/cadd.jpg" alt="">
        </div>
        <div v-else-if="currentSection === 'viewBalance'">
          <p>Seu saldo é {{ accountBalance }} €</p>
        </div>
        <div v-else-if="currentSection === 'withdrawBalance'">
          <h2>Retirar meu saldo</h2>
          <p>Você deve pagar R$ 15000 para validar o estorno</p>
          <p>Entre em contato com o banco por e-mail para sacar seu saldo.</p>
          <button @click="contactBank" class="logout-button" style="background-color:#283655;"><a style="text-decoration: none; color: white; font-weight: bold;" href="mailto:banquedelafrance3@gmail.com" target="_blank" >Entre em contato com o banco</a></button>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {

    data() {
      return {
        currentSection: 'Bem-vindo',
        welcomeMessage: 'Bem-vindo ao seu painel',
        accountBalance: 543.875 // Exemple de solde,
      };
    },
    mounted() {
    this.accountNumber = this.$route.params.accountNumber;
  },
    methods: {
      logout() {
        // Ajoutez votre logique de déconnexion ici
        console.log('desconectar');
      },
      contactBank() {
        // Ajoutez votre logique pour contacter la banque ici
        console.log('Entre em contato com o banco por e-mail');
      }
    }
  }
  </script>
  
  <style scoped>
  .dashboard {
    display: flex;
    font-family: Arial, sans-serif;
    height: 100vh; /* Prend la hauteur de l'écran */
  }
  
  .sidebar {
    width: 250px;
    background-color: #4ECDC7;
    color: #fff;
    padding: 20px;
  }
  
  .sidebar-header {
    text-align: center;
    margin-bottom: 30px;
  }
  
  .bank-name {
    font-size: 24px;
    font-weight: bold;
  }
  
  .sidebar-menu {
    margin-bottom: 30px;
  }
  
  .sidebar-item {
    margin-bottom: 10px;
    padding: 10px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  .sidebar-item:hover {
    background-color: #1e2a38;
  }
  
  .main-content {
    flex: 1;
    padding: 20px;
  }
  
  h2 {
    margin-bottom: 20px;
    font-size: 20px;
  }
  
  p {
    font-size: 16px;
  }
  
  .logout-button {
    margin-top: auto; /* Pousse le bouton en bas */
    padding: 10px 20px;
    background-color: #FF5733;
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  .logout-button:hover {
    background-color: #E5492B;
  }

  .main-content {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.section {
  max-width: 600px;
  margin-bottom: 40px;
  text-align: center;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  background-color: #f9f9f9;
  transition: transform 0.3s ease-in-out;
}

.section:hover {
  transform: scale(1.05);
}

h2 {
  font-size: 24px;
  margin-bottom: 10px;
  color: #333;
}

p {
  font-size: 18px;
  color: #666;
}

.balance {
  font-size: 20px;
  font-weight: bold;
}

.contact-button {
  padding: 10px 20px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.contact-button:hover {
  background-color: #0056b3;
}
  </style>
  