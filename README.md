<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Virtual Assistant Hub</title>
  <style>
    /* Include CSS-ul din fișierul tău Vue */
    /* Copiază direct aici CSS-ul tău */
  </style>
</head>
<body>
  <div id="app"></div>
  <script src="https://unpkg.com/vue@3"></script>
  <script>
    // Copiază scriptul din fișierul Vue și convertește-l într-un script JS simplu.
    const app = Vue.createApp({
      data() {
        return {
          backgroundImage: "https://images.unsplash.com/photo-1498050108023-c5249f4df085?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwzNjUyOXwwfDF8c2VhcmNofDV8fHRlY2hub2xvZ3l8ZW58MHx8fHwxNjg4MjkwNzI4&ixlib=rb-4.0.3&q=80&w=1920",
          agents: [
            { id: "5mz0QGMTS6vciobpmiXO", visible: false },
            { id: "sNEfrsQUklzPW2Hu6VGg", visible: false },
            { id: "EU4z5Ma0f0dHLY6m9KSq", visible: false },
            { id: "Hd79ohSgVoA9LkZcEhRG", visible: false }
          ]
        };
      },
      methods: {
        toggleWidget(index) {
          this.agents[index].visible = !this.agents[index].visible;
        }
      },
      mounted() {
        const script = document.createElement('script');
        script.src = "https://elevenlabs.io/convai-widget/index.js";
        script.async = true;
        script.type = "text/javascript";
        document.body.appendChild(script);
      }
    });

    app.mount("#app");
  </script>
</body>
</html>
