<template>
<ul class="nav navbar-nav main">
	<li id="nav-{{item[0]}}" :class="{'active': routeSup == item[0]}" v-for="item of navItems"  @mouseenter="item.$set(3, true)" @mouseleave="item.$set(3, false)">
		<a v-link="{name: item[2] ? item[2][0][0] : item[0]}">
			<span class="nav-{{item[0]}} "></span>
			<span>{{item[1]}}</span>
		</a>
		<div v-if="item[2] !== undefined">
			<ul class="sub" v-show="item[3]" transition="bounce">
				<li id="nav-{{item[0]}}-{{sub[0]}}" :class="{'active' : routeSub == sub[0]}" v-for="sub of item[2]" :style="{transition: `all 0.4s ease-out ${$index * 0.08}s`}">
					<a v-link="{name: sub[0]}" v-text="sub[1]"></a>
				</li>
			</ul>
		</div>
	</li>
</ul>
</template>																
<script>
	export default {
		data () {
			return {
				navItems: [
					['sys', '系统管理', [
						['line', '线路和车站管理'],
						['config', '系统设置']
					], false],
					['user', '权限管理', [
						['user', '用户管理'],
						['role', '角色管理'],
						['level', '用户优先级定义']
					], false],
					['device', '设备管理', [
						['list', '设备列表'],
						['zone', '摄像机分区'],
						['video', '电视墙']
					], false],
					['store', '存储管理']
				]
			}
		},
		computed: {
			routeSup () {
				return this.$route.path.split('/')[1];
			},
			routeSub () {
				return this.$route.path.split('/')[2];
			}
		}
	}
</script>
<style lang="less">
	.main{
		border-left: 1px solid #22272b; border-right: 1px solid #3a4249;
		&>li>a{
			position: absolute; width: 148px; z-index: 3000; 
		}
        &>li{
            width: 148px; float: left; height: 50px; line-height: 50px; background: #2a333a;
            text-align: center; border-right: 1px solid #22272b; border-left: 1px solid #3a4249; position: relative;
            &:hover{
            	background: #21272c;
            }
       		&.active{
       			border-bottom: 3px solid #159fb6; height: 50px; background: #15191c;
       		}
        }
        li a {color: #fff; display: block;}
        a span {display: inline-block; vertical-align: top; font-size: 14px; height: 20px;}
        .sub{    
        	position: absolute; left: 0; text-align: center; z-index: 2500; top: 50px;
			&>li{
				height: 40px; line-height: 20px; text-align: center; background: #4b4a4a; border-bottom: 3px solid transparent;
			}
			& a{width: 148px; height: 40px; font-size: 12px; font-family: "宋体"; padding: 10px 0; display: block;
				&:hover{background: #159fb6 !important; box-shadow: inset 0 1px 1px 0px rgba(42, 51, 58, 0.75);}
			}
			.active{
				border-bottom: 3px solid #159fb6; background: #21272c;
			}
        }
		.nav-sys,.nav-device,.nav-store{width:24px; height: 24px; margin:12px 10px 0 0;}
		.nav-sys{background: url(../assets/images/pic/nav-sys.png) no-repeat 0 0;}
		.nav-device{background: url(../assets/images/pic/nav-device.png) no-repeat 0 0;}
		.nav-store{background: url(../assets/images/pic/nav-store.png) no-repeat 0 0;}
	}
	
	@keyframes bounce-out {
		100% {
			top: -120px;
		}
	}
	.bounce-enter {
		&>li{
	  		transform: rotateY(180deg);
	  		opacity: 0;
		}
	}
	.bounce-leave {
		&>li{
	  		transform: rotateY(-180deg);
	  		opacity: 0;
		}
		&.sub{z-index: 4000 !important;}
		animation: bounce-out 1s ease;
	}
</style>