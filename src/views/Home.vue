<template>
<div class="container">
  <title>{{cache.name}}: Homepage</title>
   <div class="profile">
     <div class="bio" style="padding:45px;">
       <div class="title">Hello, welcome to my website! I'm <span>{{cache.name}}</span></div>
       <div class="pr">{{cache.bio}}</div>
       <div class="icons">
         <a :href="cache.links.discord" class="fab fa-discord"></a>
          <a :href="cache.links.twitter" class="fa fa-twitter"></a>
         <a :href="cache.links.github" class="fa fa-github"></a>
          <a :href="cache.links.instagram" class="fa fa-instagram"></a>
       </div>
     </div> 
     <div class="badge" style="margin:45px;text-align:center;display:grid;place-items:center;">
      <center><img :style="imgStyler('border-radius:90%;border:2px solid {status}')" height="85" width="85" :src="cache.discord.userAvatar" alt="Avatar Icon" class="avatar"> </center>
      <div class="nick">
       <span class="name">{{cache.discord.userName}}</span> <span class="hash">#{{cache.discord.userDiscriminator}}</span>
      </div>
      <div v-if="cache.discord.presence.spotify" class="spotifyStatus">
        <div class="ly1">
          <div class="h">Listening to Spotify</div>
          <i class="fa fa-spotify h2"></i>
        </div>
        <div class="ly2">
          <img :src="cache.discord.presence.spotify.songImage" alt="Song Image" class="image">
          <div class="details">
            <span class="title">{{cache.discord.presence.spotify.songName}}</span>
          <span>
              by {{cache.discord.presence.spotify.songAuthor}}
          </span>
          <span>
            on {{cache.discord.presence.spotify.songAlbum}}
          </span>

          </div>
        </div>
      </div>
      <div v-if="!cache.discord.presence.spotify" style="width:284px;height:25px;background: #121315;border-radius:0 0 15px 15px;"></div>
     </div>
   </div>
</div>
</template>


  <script>
  import conf from "../config/5.json";
    export default{
      name:'Home',
      data() {
    return {
      cache: conf
    }
  },
      mounted(){
        console.log("CACHE", this.cache)
      },
      methods:{
        imgStyler(i){
          var st = this.cache.discord.userStatus;
          switch(st){
            case "dnd":
              return i.replace("{status}", "red") 
          
            case "online":
              return i.replace("{status}", "green")
              
            case "offline":
              return i.replace("{status}", "gray")
            
            case "idle":
              return i.replace("{status}", "yellow")
             
          }
        }
      }
    }
  </script>
