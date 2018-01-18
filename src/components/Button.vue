<template>
  <div>
    <button class="btn" :class="btnData.styleClass"
    v-on:click="clickEvent()"
    >{{btnData.name}}</button>
  </div>

</template>
<script>
export default {
  name: 'btn',
  props: [
    'btnData'
  ],
  data () {
    return {
    }
  },
  methods: {
    clickEvent: function () {
      this.$emit('clickEvent')
    }
  }
}
</script>
<style lang="scss">
.btn {
	border: none;
	font-family: inherit;
	font-size: inherit;
	color: inherit;
	background: none;
	cursor: pointer;
	padding: 25px 80px;
	display: inline-block;
	margin: 15px 30px;
	text-transform: uppercase;
	letter-spacing: 1px;
	font-weight: 700;
	outline: none;
	position: relative;
	-webkit-transition: all 0.3s;
	-moz-transition: all 0.3s;
	transition: all 0.3s;
  border-radius: 5px;
  color: #fff;
  width: 15rem;

  &.active {
    box-shadow: unset;
	  top: unset;
    background-color: #fff;
    color: #000;
    border: 1px solid;
  }
}

.btn:after {
	content: '';
	position: absolute;
	z-index: -1;
	-webkit-transition: all 0.3s;
	-moz-transition: all 0.3s;
	transition: all 0.3s;
}


/* Button 1 */
.btn-red {
	background: #cb4e4e;
	box-shadow: 0 6px #ab3c3c;
  &:active{
    box-shadow: 0 0 #ab3c3c;
	  top: 6px;
  }
}

.btn-red:hover {
	box-shadow: 0 8px #ab3c3c;
	top: -2px;
}

/* Button 2 */
.btn-blue {
	background: #0e83cd;
	box-shadow: 0 6px #085a8e;

  &:active {
    box-shadow: 0 0 #085a8e;
	  top: 6px;
  }

}

.btn-blue:hover {
	box-shadow: 0 8px #085a8e;
	top: -2px;
}

/* Button 3 */
.btn-orange {
	background: #fcad26;
	box-shadow: 0 6px #b17713;

  &:active {
    	box-shadow: 0 0 #b17713;
	    top: 6px;
  }
}

.btn-orange:hover {
	box-shadow: 0 8px #b17713;
	top: -2px;
}

/* Button 4 */
.btn-green {
	background: #17954c;
	box-shadow: 0 6px #0f6131;
  &:active {
    box-shadow: 0 0 #0f6131;
	  top: 6px;
  }
}

.btn-green:hover {
	box-shadow: 0 8px #0f6131;
	top: -2px;
}
</style>
