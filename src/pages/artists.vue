<template lang="html">
  <div class="artists">
      <ul class="list">
        <router-link tag="li" :to="{name:'ArtistsDetails',params:{avatar:item.avatar_s500,name:item.name,ting_uid:item.ting_uid}}" :key="index" class="artist" v-for="(item,index) in artistsData">
          <div class="pic">
          	
            <img :alt="item.name" :src="item.avatar">
          </div>
          <div class="info">
            <div>{{ item.name }}</div>
          </div>
          
        </router-link>
      </ul>
    </div>
</template>

<script>
export default {
  name:"artists",
  data(){
    return{
       artistsArr:[],
       artistsData:[]
    }
  },
  mounted(){
  	const URL = this.HOST + "/v1/restserver/ting?method=baidu.ting.billboard.billList&type=1&size=10&offset=0";
      this.$axios.get(URL)
        .then(res => {
        	console.log(res);
        	for(var i = 0;i<res.data.song_list.length;i++){
        		this.artistsArr.push({
            	ting_uid:res.data.song_list[i].ting_uid,
          	})
        	}
          console.log(this.artistsArr);
          
          for(var i =0;i<this.artistsArr.length;i++){
		    	console.log("--"+this.artistsArr[i].ting_uid);
		      const artistsURL = this.HOST + "/v1/restserver/ting?method=baidu.ting.artist.getInfo&tinguid="+ this.artistsArr[i].ting_uid;
		      this.$axios.get(artistsURL)
		        .then(res => {
		        	//console.log(res);
		          this.artistsData.push({
		            avatar:res.data.avatar_s500,
		            name:res.data.name,
		            ting_uid:res.data.ting_uid
		          })
		        })
        .catch(error => {
          console.log(error);
        })
    	}
          
        })
        .catch(error => {
          console.log(error);
     })
    
    
    /*for(var i =0;i<this.artistsArr.length;i++){
    	console.log("--"+this.artistsArr[i].ting_uid);
      const artistsURL = this.HOST + "/v1/restserver/ting?method=baidu.ting.artist.getInfo&tinguid="+ this.artistsArr[i].ting_uid;
      this.$axios.get(artistsURL)
        .then(res => {
        	//console.log(res);
          this.artistsData.push({
            avatar:res.data.avatar_s500,
            name:res.data.name,
            ting_uid:res.data.ting_uid
          })
        })
        .catch(error => {
          console.log(error);
        })
    }*/
    //console.log("--"+this.artistsData);
  }
}
</script>

<style scoped>

.artists{
  padding: 0 17px;
  background: #fff;
}

.list li {
    padding-left: 0;
    min-height: 70px;
    display: flex;
    align-items: center;
    border-bottom: 1px solid #F2F2F2;
}

.pic{
  width: 54px;
  height: 54px;
  margin-right: 15px;
}

.info {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: flex-start;
    font-size: 16px;
}

.pic img{
  border-radius: 27px;
  overflow: hidden;
}


</style>
