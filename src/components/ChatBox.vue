<template>
  <div class="chatbox-container">
    <div class="container">
      <h1>Чат бот</h1>
      <div class="messageBox mt-8" id="scrollContainer">
        <template v-for="(message, index) in messages" :key="index">
          <div :class="message.from == 'user' ? 'messageFromUser' : 'messageFromChat'">
            <div :class="message.from == 'user' ? 'userMessageWrapper' : 'chatMessageWrapper'">
              <div :class="message.from == 'user' ? 'userMessageContent' : 'chatMessageContent'" id="aaa">
                {{ message.data }}
              </div>
            </div>
          </div>
        </template>
      </div>
      <div class="answerContainer">
        <button
            @click="sendMessage('Заказать пиццу')"
            class="answerButton">
          Заказать пиццу
        </button>
        <button
          @click="sendMessage('Установить будильник')"
          class="answerButton"
        >
          Установить будильник
        </button>
        <button
            @click="sendMessage('Вывести погоду')"
            class="answerButton">
          Вывести погоду
        </button>
      </div>
      <div class="inputContainer">
        <input
          @keyup.enter="sendMessage(currentMessage)"
          v-model="currentMessage"
          type="text"
          class="messageInput"
          placeholder="Попроси меня..."
        />
        <button
            @click="sendMessage(currentMessage)"
            class="askButton">
          Отправить
        </button>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: "ChatBox",

  data() {

    return {
      currentMessage: "",
      messages: [
        {
          from: "chat",
          data: "Привет! Я чат бот. Попроси меня о чём-то",
        }
      ],
    };
  },

  mounted(){
    this.scrollToBottom()
  },

  updated(){
    this.scrollToBottom()
  },

  methods: {

    sendMessage(message) {
      if (message) {
        this.messages.push({
          from: "user",
          data: message,
        });
        let answer = "Хорошо.";
        switch (message) {
          case "Заказать пиццу":
            answer = "Хорошо, я закажу пиццу.";
            break;
          case "Установить будильник":
            answer = "Хорошо, я установлю будильник.?";
            break;
          case "Вывести погоду":
            answer = "Хорошо, я выведу погоду.";
            break;
        }
        this.messages.push({
          from: "chat",
          data: answer + " Что еще могу сделать?",
        });

        this.currentMessage = "";
      }
    },

    scrollToBottom(){
        const container = this.$el.querySelector("#scrollContainer");
        container.scrollTop = container.scrollHeight;
    }
  },

};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@400;500&display=swap");

.chatbox-container {
  position: fixed;
  bottom: 24px;
  right: 24px;
  z-index: 1000;
}

.container {
  width: 400px;
  height: 600px;
  background-color: white;
  border-radius: 8px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
  overflow: hidden;
  font-family: "Roboto", sans-serif;
}

.answerContainer {
  padding: 10px;
  display: flex;
  align-items: center;
  justify-content: space-around;
}

.answerButton {
  background-color: #1877f2;
  color: white;
  font-size: 16px;
  padding: 8px 16px;
  border: none;
  outline: none;
  cursor: pointer;
  border-radius: 24px;
  transition: background-color 0.3s ease-in-out;
}
.answerButton:hover {
  background-color: #145cb3;
}

h1 {
  font-size: 24px;
  font-weight: 500;
  text-align: center;
  color: #222;
  padding: 16px;
  margin: 0;
  background-color: #f7f7f7;
  border-bottom: 1px solid #e7e7e7;
}

.messageFromChat {
  display: flex;
}

.messageBox {
  display: flex;
  max-height: 400px;
  overflow-y: auto;
  padding: 16px;
  border-top: 1px solid #f0f0f0;
  border-bottom: 1px solid #f0f0f0;
  flex-grow: 1;
  flex-direction: column;
  gap: 12px;
 }

.messageFromUser {
  display: flex;
  align-items: center;
  justify-content: flex-end;
}
.messageFromChat {
  display: flex;
  margin-bottom: 8px;
}

.userMessageWrapper {
  display: flex;
  align-items: center;
  justify-content: flex-end;
}
.chatMessageWrapper {
  display: flex;
  flex-direction: column;
  opacity: 0;
  animation: ani 2.5s forwards;
}

@keyframes ani {
  0% {opacity: 0;}
  100% {opacity: 1;}
}

.userMessageWrapper {
  align-self: flex-end;
}

.chatMessageWrapper {
  align-self: flex-start;
}

.userMessageContent,

.chatMessageContent {
  max-width: 60%;
  padding: 8px 12px;
  border-radius: 18px;
  margin-bottom: 2px;
  font-size: 14px;
  line-height: 1.4;
}

.userMessageContent {
  background-color: #1877f2;
  color: white;
  border-top-right-radius: 0;
}

.chatMessageContent {
  background-color: #ededed;
  color: #222;
  border-top-left-radius: 0;
}

.inputContainer {
  display: flex;
  align-items: center;
  padding: 8px;
  background-color: #f0f0f0;
}

.messageInput {
  flex-grow: 1;
  border: none;
  outline: none;
  padding: 12px;
  font-size: 16px;
  background-color: white;
  border-radius: 24px;
  margin-right: 8px;
}

.askButton {
  background-color: #1877f2;
  color: white;
  font-size: 16px;
  padding: 8px 16px;
  border: none;
  outline: none;
  cursor: pointer;
  border-radius: 24px;
  transition: background-color 0.3s ease-in-out;
}

.askButton:hover {
  background-color: #145cb3;
}

@media (max-width: 480px) {
  .container {
    width: 100%;
    max-width: none;
    border-radius: 0;
  }
}
.chatbox-container {
  position: fixed;
  bottom: 24px;
  right: 24px;
  z-index: 1000;
}

.messageFromUser,
.messageFromChat {
  display: flex;
}
</style>
