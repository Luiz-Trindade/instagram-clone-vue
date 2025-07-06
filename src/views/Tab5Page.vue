<template>
  <ion-page>
    <ion-content :fullscreen="true">
      <!-- Loop através dos posts -->
      <ion-card v-for="post in posts" :key="post.id"
        style="margin: 0; border-radius: 0; box-shadow: none; margin-bottom: 20px;">
        <!-- Cabeçalho do card (usuário) -->
        <ion-card-header>
          <ion-item lines="none">
            <ion-avatar slot="start">
              <img :src="post.user.avatar" />
            </ion-avatar>
            <ion-label>
              <h3>{{ post.user.username }}</h3>
              <p>{{ post.location }}</p>
            </ion-label>
            <ion-icon :icon="ellipsisHorizontal" slot="end"></ion-icon>
          </ion-item>
        </ion-card-header>

        <!-- Imagem da postagem -->
        <div class="post-image-wrapper">
          <img class="post-image" :src="post.imageUrl" />
        </div>

        <!-- Área de interação (curtir, comentar, etc.) -->
        <ion-card-content>
          <div class="post-actions">
            <ion-button fill="clear" size="small" @click="toggleLike(post)">
              <ion-icon :icon="post.isLiked ? heart : heartOutline" size="large"
                :color="post.isLiked ? 'danger' : ''"></ion-icon>
            </ion-button>
            <ion-button fill="clear" size="small">
              <ion-icon :icon="chatbubbleOutline" size="large"></ion-icon>
            </ion-button>
            <ion-button fill="clear" size="small">
              <ion-icon :icon="sendOutline" size="large"></ion-icon>
            </ion-button>
            <ion-button fill="clear" size="small" class="save-icon">
              <ion-icon :icon="bookmarkOutline" size="large"></ion-icon>
            </ion-button>
          </div>

          <p class="likes">{{ formatLikes(post.likes) }} curtidas</p>

          <p class="caption">
            <strong>{{ post.user.username }}</strong> {{ post.caption }}
          </p>

          <p class="comments">Ver todos os {{ post.comments }} comentários</p>
          <p class="time">{{ formatTime(post.timestamp) }}</p>
        </ion-card-content>
      </ion-card>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import {
  IonPage,
  IonContent,
  IonCard,
  IonCardHeader,
  IonCardContent,
  IonItem,
  IonAvatar,
  IonLabel,
  IonIcon,
  IonButton
} from '@ionic/vue';
import {
  heartOutline,
  heart,
  chatbubbleOutline,
  sendOutline,
  bookmarkOutline,
  ellipsisHorizontal
} from 'ionicons/icons';

// Interface para tipagem
interface Post {
  id: number;
  user: {
    username: string;
    avatar: string;
  };
  location: string;
  imageUrl: string;
  caption: string;
  likes: number;
  comments: number;
  timestamp: string;
  isLiked: boolean;
}

// Lista de posts
const posts = ref<Post[]>([
  {
    id: 1,
    user: {
      username: "ionic_dev",
      avatar: "https://i.pravatar.cc/150?img=32"
    },
    location: "São Paulo, Brasil",
    imageUrl: "https://images.unsplash.com/photo-1517849845537-4d257902454a",
    caption: "Aprendendo a criar interfaces com Ionic! #ionic #frontend #mobile",
    likes: 1234,
    comments: 56,
    timestamp: "2023-05-15T14:30:00",
    isLiked: false
  },
  {
    id: 2,
    user: {
      username: "vue_lover",
      avatar: "https://i.pravatar.cc/150?img=12"
    },
    location: "Rio de Janeiro, Brasil",
    imageUrl: "https://images.unsplash.com/photo-1551650975-87deedd944c3",
    caption: "Explorando as maravilhas do Vue 3! #vue #javascript #frontend",
    likes: 892,
    comments: 23,
    timestamp: "2023-05-14T09:15:00",
    isLiked: true
  },
  {
    id: 3,
    user: {
      username: "web_designer",
      avatar: "https://i.pravatar.cc/150?img=45"
    },
    location: "Belo Horizonte, Brasil",
    imageUrl: "https://images.unsplash.com/photo-1547658719-da2b51169166",
    caption: "Novo projeto de UI/UX finalizado! #design #ui #ux",
    likes: 2456,
    comments: 128,
    timestamp: "2023-05-12T18:45:00",
    isLiked: false
  },
  {
    id: 4,
    user: {
      username: "mobile_guru",
      avatar: "https://i.pravatar.cc/150?img=21"
    },
    location: "Curitiba, Brasil",
    imageUrl: "https://images.unsplash.com/photo-1506744038136-46273834b3fb",
    caption: "Testando novos recursos do Ionic Vue! #mobile #ionicvue",
    likes: 678,
    comments: 12,
    timestamp: "2023-05-13T11:20:00",
    isLiked: false
  },
  {
    id: 5,
    user: {
      username: "frontend_master",
      avatar: "https://i.pravatar.cc/150?img=7"
    },
    location: "Fortaleza, Brasil",
    imageUrl: "https://images.unsplash.com/photo-1465101046530-73398c7f28ca",
    caption: "Componentização é vida! #frontend #vuejs",
    likes: 1532,
    comments: 67,
    timestamp: "2023-05-11T16:00:00",
    isLiked: true
  },
  {
    id: 6,
    user: {
      username: "code_artist",
      avatar: "https://i.pravatar.cc/150?img=18"
    },
    location: "Recife, Brasil",
    imageUrl: "https://images.unsplash.com/photo-1519125323398-675f0ddb6308",
    caption: "Arte e código juntos! #creative #coding",
    likes: 321,
    comments: 8,
    timestamp: "2023-05-10T08:30:00",
    isLiked: false
  },
  {
    id: 7,
    user: {
      username: "tech_girl",
      avatar: "https://i.pravatar.cc/150?img=47"
    },
    location: "Brasília, Brasil",
    imageUrl: "https://images.unsplash.com/photo-1465101178521-c1a9136a3b99",
    caption: "Participando de um hackathon incrível! #hackathon #tech",
    likes: 987,
    comments: 34,
    timestamp: "2023-05-09T19:45:00",
    isLiked: false
  },
  {
    id: 8,
    user: {
      username: "dev_junior",
      avatar: "https://i.pravatar.cc/150?img=14"
    },
    location: "Salvador, Brasil",
    imageUrl: "https://images.unsplash.com/photo-1519125323398-675f0ddb6308",
    caption: "Primeiro app publicado! #devlife #conquista",
    likes: 412,
    comments: 15,
    timestamp: "2023-05-08T13:10:00",
    isLiked: false
  }
]);

// Função para alternar curtida
const toggleLike = (post: Post) => {
  post.isLiked = !post.isLiked;
  post.likes += post.isLiked ? 1 : -1;
};

// Função para formatar números de curtidas
const formatLikes = (likes: number): string => {
  if (likes >= 1000) {
    return (likes / 1000).toFixed(1) + 'k';
  }
  return likes.toString();
};

// Função para formatar o tempo da postagem
const formatTime = (timestamp: string): string => {
  const now = new Date();
  const postDate = new Date(timestamp);
  const diffInHours = Math.floor((now.getTime() - postDate.getTime()) / (1000 * 60 * 60));

  if (diffInHours < 1) {
    const diffInMinutes = Math.floor(diffInHours * 60);
    return `HÁ ${diffInMinutes} MINUTO${diffInMinutes !== 1 ? 'S' : ''}`;
  } else if (diffInHours < 24) {
    return `HÁ ${diffInHours} HORA${diffInHours !== 1 ? 'S' : ''}`;
  } else {
    const diffInDays = Math.floor(diffInHours / 24);
    return `HÁ ${diffInDays} DIA${diffInDays !== 1 ? 'S' : ''}`;
  }
};
</script>

<style scoped>
/* Seus estilos anteriores permanecem os mesmos */
ion-card {
  margin: 0;
  border-radius: 0;
  box-shadow: none;
}

ion-avatar {
  width: 32px;
  height: 32px;
  margin-right: 12px;
}

.post-image-wrapper {
  display: flex;
  justify-content: center;
  width: 100%;
}

.post-image {
  width: 100%;
  max-width: 500px;
  height: auto;
  border-radius: 10px;
  object-fit: cover;
}

.post-actions {
  display: flex;
  padding-bottom: 8px;
}

.post-actions ion-icon {
  margin-right: 16px;
}

.save-icon {
  margin-left: auto;
  margin-right: 0;
}

.likes,
.caption,
.comments,
.time {
  margin: 4px 0;
}

.likes {
  font-weight: bold;
}

.caption {
  line-height: 1.4;
}

.comments {
  color: #8e8e8e;
}

.time {
  color: #8e8e8e;
  font-size: 0.8em;
  text-transform: uppercase;
}

/* Responsividade */
@media (max-width: 600px) {
  .post-image {
    max-width: 100vw;
    border-radius: 0;
  }

  ion-card {
    border-radius: 0;
  }
}
</style>