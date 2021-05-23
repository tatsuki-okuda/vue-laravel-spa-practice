<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-sm-6">
              <!-- https://jp.vuejs.org/v2/guide/events.html#%E3%82%A4%E3%83%99%E3%83%B3%E3%83%88%E4%BF%AE%E9%A3%BE%E5%AD%90 -->
                <form v-on:submit.prevent="submit">
                    <div class="form-group row">
                        <label for="title" class="col-sm-3 col-form-label">Title</label>
                        <input type="text" class="col-sm-9 form-control" id="title" v-model="task.title">
                    </div>
                    <div class="form-group row">
                        <label for="content" class="col-sm-3 col-form-label">Content</label>
                        <input type="text" class="col-sm-9 form-control" id="content" v-model="task.content">
                    </div>
                    <div class="form-group row">
                        <label for="person-in-charge" class="col-sm-3 col-form-label">Person In Charge</label>
                        <input type="text" class="col-sm-9 form-control" id="person-in-charge" v-model="task.person_in_charge">
                    </div>
                    <button type="submit" class="btn btn-primary">Submit</button>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
      data: function() {
        return {
          task: {}
        }
      },
      methods: {
        submit(){
          axios.post('/api/tasks', this.task)
            .then( res => {
              console.log('ok');
              // console.log(this);
              // vueで作ったtask.listのルーティングを呼び出してリダイレクトしている。
              // https://router.vuejs.org/ja/guide/essentials/navigation.html
              // vueインスタンスに$マークがついてメソッドが格納されている。
              this.$router.push({name: 'task.list'});
            })
            .catch(e =>{
              console.log('error');
            })
        }
      }
    }
</script>