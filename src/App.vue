<template>
  <div id="app">
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width" />
    <link rel="icon" href="@/assets/images/Fallen.png" />
    <div class="navbar">
      <div class="logo">Fallen</div>
      <div class="content">
        <router-link to="/">
          <div class="item"><i class="fa fa-home"></i> Homepage</div>
        </router-link>
          <a href="https://api-bioprc.glitch.me/">
          <div class="item"><i class="fa fa-code"></i> API</div>
        </a>
        <a href="https://github.com/maze357/vue-portfolio">
          <div class="item"><i class="fa fa-github"></i> Source</div>
        </a>
        
        <router-link to="works">
          <div class="item"><i class="fa fa-hammer"></i> Projects</div>
        </router-link>
        <a href="https://discord.gg/1958">
          <div class="item">
            <i style="font-weight: 400 !important" class="fab fa-discord"></i>
            Discord
          </div>
        </a>
      </div>
      <div class="end">
        <i id="bc15" class="fa fa-align-justify"></i>
      </div>
    </div>
      <router-view></router-view>
    <div class="footer">
      <p style="font-size: 13px">© 2021 - <span> All Rights Reserved </span></p>
    </div>
  </div>
</template>
<script>
import conf from "./config/5.json";
import { post } from "axios";
export default {
  name: "App",
  data() {
    return {
      cache: conf
    }
  },
  mounted() {
    post(
      `${this.cache.A_POINT}/getUser?ref=` + this.cache.name,
      {},
      {
        headers: {
          Authorization: "Basic " + this.cache.discord.id,
        },
      }
    ).then((response) => {
      this.cache.discord = {
        userDiscriminator: response.data.userDiscriminator,
        userID: response.data.userID,
        userName: response.data.userName,
        userAvatar: response.data.userAvatar,
        userStatus: response.data.userStatus,
        presence:{}
      };
    });
      post(
      `${this.cache.A_POINT}/getUserState?identify=spotify&ref=` + this.cache.name,
      {},
      {
        headers: {
          Authorization: "Basic " + this.cache.discord.id,
        },
      }
    ).then((response) => {
      console.log(response.data)
      this.cache.discord.presence = {
        spotify:{
          songName:response.data.userState.songName, 
          songAlbum:response.data.userState.songAlbum,
          songAuthor:response.data.userState.songAuthor, 
          songImage:response.data.userState.songImage
        }
      };
    });
  },
};
</script>

<style>
@import "./styles/main.css";
</style>
