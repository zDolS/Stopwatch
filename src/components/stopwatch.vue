
<template>
  <!-- Добавляем контейнер для секундомера -->
  <div class="timerContaner">
    <!-- добавляем часы -->
    <p class="stopwatchTimer inactive" v-bind:class="{active: isActive}">{{formattedElapsedTime}}</p>
    <!-- добавляем линию посредине -->
    <div class="line inactive" v-bind:class="{active: isActive}"></div>
    <!-- кнопка паузы-->
    <div @click="pause" class="buttonPause" v-bind:class="{active: isActive}">
      <!-- не самое лучшие решение, кнопка pause через два отдельных дива, с двумя отдельными линиями-->
      <div class="linePause" v-bind:class="{active: isActive}">
      <div class="linePauseTwo" v-bind:class="{active: isActive}"></div></div></div>
      <!-- кнопка сброса -->
    <div @click="reset" ><div class="buttonReset inactive" v-bind:class="{active: isActive}"></div></div>
    <!-- кнопка старта -->
    <div @click="start" class="buttonPlay inactive" v-bind:class="{active: isActive}"></div>  
  </div>
</template>

<script>
export default {
    data: () => ({    
      // стартовое количество секунд
        elapsedTime: 0,
      // состояние стиля, по умолнанию не активное состояние
        isActive: false, 
    }),
    computed: {
      // отслеживамое состоние прошедших секунд
      formattedElapsedTime: function ()  {
        // сохдаем переменную и внее записоваем стартовое состояние отчета времени
        const date = new Date(null);
        // задаем стартовое количество секунд, которые в дальнейшем при использование метода start() будут увеличиваться
        date.setSeconds(this.elapsedTime);
        // условаия на отображение секунд минут и часов
        if (date.getMinutes() > 0) {
          return date.getMinutes() + ":" + date.getSeconds();
        }
        else if((date.getSeconds() > 0) && (date.getSeconds() < 10) && (date.getMinutes() > 0)) {
        return "0" + date.getSeconds();
        }
        else if(date.getUTCHours() > 0) {
          return date.getHours() + ":" +  date.getMinutes() + ":" + date.getSeconds();
        }
        else return date.getSeconds();
      }
    },
    methods: {
      // метод старта отсчета секунд и помимо этого переводит стили в активное состояние(подсветка)
      start() {
        this.timer = setInterval(() => {
          this.elapsedTime += 1;
        }, 1000);
        this.isActive = true;
      },
      // метод сброса секундомера, обнуляем количество секунд и останавливаем счетчий времени, возрашаем стили в исходное состояние 
      reset() {
        this.elapsedTime = 0;
        clearInterval(this.timer);
        this.isActive = false;
      },
      // останавливаем счетчий времени, возрашаем стили в исходное состояние 
      pause() {
        clearInterval(this.timer);
        this.isActive = false;
      },
    }
  };
</script>

<style>
/*у всех стилей для внутреностей контенера секундомера два состояния, не активное и активное, в неактивном состояние описаны стили и положение
элементов, в активном состояние прячестся кнопка start и появляеться кнопка pause, помимо этого в активном состояние меняеться стиль элементов на белый. По умолчанию, до нажатия кнопки start, все стили в состояние не активны*/
/*стиль контейнера секундомера*/
.timerContaner {
  position: relative;
  width: 225px;
  height: 120px;
  margin-right: 50px;
  margin-bottom: 45px;
  background: #696969;
}
/*счетчик времени*/
.stopwatchTimer.inactive{
  position: absolute;
  width: 75px;
  height: 18px;
  left: 75px;
  top: 2px;
  font-family: Gotham Pro;
  font-style: normal;
  font-weight: normal;
  font-size: 22px;
  line-height: 21px;
  text-align: center;
  color: #9E9E9E;
}
.stopwatchTimer.active{
  color: #ffffff;
}
.line.inactive {
  position: absolute;
  width: 99%;
  height: 0px;
  top: 50%;
  border: 1px solid #9E9E9E;
}
.line.active {
  position: absolute;
  width: 99%;
  height: 0px;
  top: 50%;
  border: 1px solid #ffffff;
}
.buttonPlay.active {
  display: none;
}
.buttonPlay.inactive {
  position: absolute;
  left: 70px;
  top: 80px;
  width: 0;
  height: 0;
  border-style: solid;
  border-width: 10px 0 10px 16px;
  border-color: transparent transparent transparent #9e9e9e;
  background: #696969;
  outline: none !important;
}

.buttonReset.inactive {
  background: #9E9E9E;
  position: relative;
  width: 20px;
  height: 20px;
  left: 135px;
  top: 80px;  
}
.buttonReset.active {
  background: #ffffff;
}
.buttonPause.inactive {
  display: none;
}
.buttonPause.active {
  position: absolute; 
  width: 30px;
  height: 20px;
  left: 70px;
  top: 80px;
  background: transparent;
  border: none !important;
  outline: none !important;
}
.linePause.active {
  position: relative;
  width: 3px;
  height: 100%;
  left: 0px;
  top: 0px;
  background: #ffffff;
  outline: none !important;
}
.linePause.inactive {
  display: none;
}
.linePauseTwo.active {
  position: relative;
  width: 3px;
  height: 100%;
  left: 6px;
  top: 0px;
  background: #ffffff;
  outline: none !important;
}
.linePauseTwo.inactive {
  display: none;
}
</style>
