<template>
	<view class="container">
		<view class="login-wrapper">
			<view class="login-box">
				<text class="login-title">欢迎回来</text>
				<view class="input-group">
					<view class="input-item add_shadow">
						<input v-model="username" type="text" placeholder="输入邮箱" placeholder-class="input-placeholder" style="text-align: center;" />
					</view>
					<view class="input-item add_shadow">
						<input v-model="password" type="password" placeholder="输入密码" placeholder-class="input-placeholder"  style="text-align: center;"/>
					</view>
				</view>
				<view class="login-btn" @tap="handleLogin">
					<text class="btn-text">登录</text>
				</view>
			</view>
		</view>
				<view class="links">
					<text class="link-text" @tap="goForgetPassword">忘记密码</text>
					<text class="link-text" @tap="goSignup">注册</text>
				</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			username: '',
			password: ''
		}
	},
	methods: {
		handleLogin() {
			if (!this.username.trim()) {
				uni.showToast({
					title: '请输入用户名',
					icon: 'none'
				});
				return;
			}
			if (!this.password.trim()) {
				uni.showToast({
					title: '请输入密码',
					icon: 'none'
				});
				return;
			}
			
			uni.showLoading({
				title: '登录中...'
			});
			
			setTimeout(() => {
				uni.hideLoading();
				uni.showToast({
					title: '登录成功',
					icon: 'success'
				});
				setTimeout(() => {
					uni.switchTab({
						url: '/pages/index/index'
					});
				}, 1500);
			}, 1000);
		},
		goForgetPassword() {
			uni.showToast({
				title: '忘记密码功能开发中',
				icon: 'none'
			});
		},
		goSignup() {
			uni.showToast({
				title: '注册功能开发中',
				icon: 'none'
			});
		}
	}
}
</script>

<script module="webglModule" lang="renderjs">

const OPT = {
  sphereRad: 130,
  fLen: 300,
  maxParticle: 400,
  turnSpeed: 0.005,
  backgroundColor: "#212020"
};

let canvas, ctx, width, height, CenterX, CenterY;
let particles = [];
let animationId = null;

function Vector(x, y, z) {
  this.x = x || 0;
  this.y = y || 0;
  this.z = z || 0;
}

Vector.prototype = {
  negative: function() {
    return new Vector(-this.x, -this.y, -this.z);
  },
  add: function(v) {
    if (v instanceof Vector) return new Vector(this.x + v.x, this.y + v.y, this.z + v.z);
    else return new Vector(this.x + v, this.y + v, this.z + v);
  },
  subtract: function(v) {
    if (v instanceof Vector) return new Vector(this.x - v.x, this.y - v.y, this.z - v.z);
    else return new Vector(this.x - v, this.y - v, this.z - v);
  },
  multiply: function(v) {
    if (v instanceof Vector) return new Vector(this.x * v.x, this.y * v.y, this.z * v.z);
    else return new Vector(this.x * v, this.y * v, this.z * v);
  },
  divide: function(v) {
    if (v instanceof Vector) return new Vector(this.x / v.x, this.y / v.y, this.z / v.z);
    else return new Vector(this.x / v, this.y / v, this.z / v);
  },
  equals: function(v) {
    return this.x == v.x && this.y == v.y && this.z == v.z;
  },
  dot: function(v) {
    return this.x * v.x + this.y * v.y + this.z * v.z;
  },
  cross: function(v) {
    return new Vector(
      this.y * v.z - this.z * v.y,
      this.z * v.x - this.x * v.z,
      this.x * v.y - this.y * v.x
    );
  },
  length: function() {
    return Math.sqrt(this.dot(this));
  },
  unit: function() {
    return this.divide(this.length());
  },
  min: function() {
    return Math.min(Math.min(this.x, this.y), this.z);
  },
  max: function() {
    return Math.max(Math.max(this.x, this.y), this.z);
  },
  toAngles: function() {
    var phi = Math.atan2(this.y, this.x);
    if (phi < 0) {
      phi = phi + Math.PI * 2;
    }
    return {
      theta: Math.acos(this.z / this.length()),
      phi: phi
    };
  },
  angleTo: function(a) {
    return Math.acos(this.dot(a) / (this.length() * a.length()));
  },
  toArray: function(n) {
    return [this.x, this.y, this.z].slice(0, n || 3);
  },
  clone: function() {
    return new Vector(this.x, this.y, this.z);
  },
  init: function(x, y, z) {
    this.x = x;
    this.y = y;
    this.z = z;
    return this;
  }
};

Vector.negative = function(a, b) {
  b.x = -a.x;
  b.y = -a.y;
  b.z = -a.z;
  return b;
};
Vector.add = function(a, b, c) {
  if (b instanceof Vector) {
    c.x = a.x + b.x;
    c.y = a.y + b.y;
    c.z = a.z + b.z;
  } else {
    c.x = a.x + b;
    c.y = a.y + b;
    c.z = a.z + b;
  }
  return c;
};
Vector.subtract = function(a, b, c) {
  if (b instanceof Vector) {
    c.x = a.x - b.x;
    c.y = a.y - b.y;
    c.z = a.z - b.z;
  } else {
    c.x = a.x - b;
    c.y = a.y - b;
    c.z = a.z - b;
  }
  return c;
};
Vector.multiply = function(a, b, c) {
  if (b instanceof Vector) {
    c.x = a.x * b.x;
    c.y = a.y * b.y;
    c.z = a.z * b.z;
  } else {
    c.x = a.x * b;
    c.y = a.y * b;
    c.z = a.z * b;
  }
  return c;
};
Vector.divide = function(a, b, c) {
  if (b instanceof Vector) {
    c.x = a.x / b.x;
    c.y = a.y / b.y;
    c.z = a.z / b.z;
  } else {
    c.x = a.x / b;
    c.y = a.y / b;
    c.z = a.z / b;
  }
  return c;
};
Vector.cross = function(a, b, c) {
  c.x = a.y * b.z - a.z * b.y;
  c.y = a.z * b.x - a.x * b.z;
  c.z = a.x * b.y - a.y * b.x;
  return c;
};
Vector.unit = function(a, b) {
  var length = a.length();
  b.x = a.x / length;
  b.y = a.y / length;
  b.z = a.z / length;
  return b;
};
Vector.fromAngles = function(theta, phi) {
  return new Vector(Math.cos(theta) * Math.cos(phi), Math.sin(phi), Math.sin(theta) * Math.cos(phi));
};
Vector.randomDirection = function() {
  return Vector.fromAngles(Math.random() * Math.PI * 2, Math.asin(Math.random() * 2 - 1));
};
Vector.min = function(a, b) {
  return new Vector(Math.min(a.x, b.x), Math.min(a.y, b.y), Math.min(a.z, b.z));
};
Vector.max = function(a, b) {
  return new Vector(Math.max(a.x, b.x), Math.max(a.y, b.y), Math.max(a.z, b.z));
};
Vector.lerp = function(a, b, fraction) {
  return b.subtract(a).multiply(fraction).add(a);
};
Vector.fromArray = function(a) {
  return new Vector(a[0], a[1], a[2]);
};
Vector.angleBetween = function(a, b) {
  return a.angleTo(b);
};

var util = {
  norm: function(value, min, max) {
    return (value - min) / (max - min);
  },
  lerp: function(norm, min, max) {
    return min + norm * (max - min);
  },
  map: function(value, sourceMin, sourceMax, destMin, destMax) {
    return this.lerp(this.norm(value, sourceMin, sourceMax), destMin, destMax);
  },
  clamp: function(value, min, max) {
    return Math.min(Math.max(value, min), max);
  },
  distance: function(x0, y0, x1, y1) {
    var dx = x0 - x1;
    var dy = y0 - y1;
    return Math.sqrt(dx * dx + dy * dy);
  },
  randomRange: function(min, max) {
    return min + Math.random() * (max - min);
  },
  randomInt: function(min, max) {
    return Math.floor(min + Math.random() * (max - min + 1));
  },
  degreesToRads: function(degrees) {
    return degrees / 180 * Math.PI;
  },
  radsToDegrees: function(radians) {
    return radians * 180 / Math.PI;
  },
  roundToPlaces: function(value, places) {
    var mult = Math.pow(10, places);
    return Math.round(value * mult) / mult;
  },
  roundNearest: function(value, nearest) {
    return Math.round(value / nearest) * nearest;
  }
};

var Particle = function(add) {
  var theta;
  if (add === true) {
    theta = Math.PI / 2;
  } else {
    theta = Math.random() * Math.PI;
  }
  this.distPos = {
    theta: theta,
    phi: 2 * Math.random() * Math.PI
  };

  this.distPos.x = OPT.sphereRad * Math.sin(this.distPos.theta) * Math.cos(this.distPos.phi);
  this.distPos.y = OPT.sphereRad * Math.sin(this.distPos.theta) * Math.sin(this.distPos.phi);
  this.distPos.z = OPT.sphereRad * Math.cos(this.distPos.theta);
  this.distVec = new Vector(this.distPos.x, this.distPos.y, this.distPos.z);
  this.unitVec = this.distVec.unit();

  var startMult = 1 + Math.random() * 2;
  this.startVec = this.distVec.multiply(startMult);
  this.x = this.startVec.x;
  this.y = this.startVec.y;
  this.z = this.startVec.z;

  this.veloRate = 1 + Math.random() * 1;
  this.velo = this.unitVec.negative().multiply(this.veloRate);
  this.finalVelo = 0;
  this.m = OPT.fLen / (OPT.fLen - this.z);

  this.age = this.life = 50 + Math.floor(Math.random() * 500);
  this.proj = {};
  this.turnAngle = 0;
  this.wanderTime = 200;
  this.radius = 1 + Math.random() * 3;

  const colors = [
    "rgba(255,100,100,",
    "rgba(255,160,80,",
    "rgba(100,180,255,",
    "rgba(100,255,100,",
    "rgba(200,150,255,",
    "rgba(255,200,80,",
    "rgba(100,255,200,",
    "rgba(255,150,200,",
    "rgba(255,255,100,"
  ];
  this.color = colors[Math.floor(Math.random() * colors.length)];
};

Particle.prototype.update = function() {
  this.nowPos = new Vector(this.x, this.y, this.z);
  this.nowPosUnit = this.nowPos.unit();

  if (this.wanderTime > 0 && this.nowPos.length() > (OPT.sphereRad * 1.2)) {
    this.wanderTime--;
    this.velo.x += 0.1 * (Math.random() * 2 - 1);
    this.velo.y += 0.1 * (Math.random() * 2 - 1);
    this.velo.z += 0.1 * (Math.random() * 2 - 1);
    this.x = this.x + this.velo.x;
    this.y = this.y + this.velo.y;
    this.z = this.z + this.velo.z;
    this.op = util.map(this.nowPos.length(), OPT.sphereRad, this.startVec.length(), 1, 0);

  } else if (this.nowPos.length() > OPT.sphereRad) {
    if (this.finalPos === 0) {
      this.finalPos = this.nowPosUnit.multiply(OPT.sphereRad);
    }
    if (this.finalVelo === 0) {
      this.finalVelo = this.nowPosUnit.negative().multiply(this.veloRate);
    }
    this.x = this.x + this.finalVelo.x;
    this.y = this.y + this.finalVelo.y;
    this.z = this.z + this.finalVelo.z;
    this.op = util.map(this.nowPos.length(), OPT.sphereRad, this.startVec.length(), 1, 0);
  } else {
    this.op = this.life / (this.age / 2);
    this.turnAngle = (this.turnAngle + OPT.turnSpeed) % (Math.PI * 2);
    var cosAngle = Math.cos(OPT.turnSpeed);
    var sinAngle = Math.sin(OPT.turnSpeed);
    this.x = cosAngle * this.nowPos.x + sinAngle * this.nowPos.z;
    this.z = -sinAngle * this.nowPos.x + cosAngle * this.nowPos.z;
    this.y = this.nowPos.y;
    this.life--;
  }

  this.m = OPT.fLen / (OPT.fLen - this.z);
};

function loop() {
  ctx.fillStyle = OPT.backgroundColor;
  ctx.fillRect(0, 0, width, height);
  
  if (particles.length < OPT.maxParticle) {
    var p = new Particle();
    particles.push(p);
  }
  for (var i = 0; i < particles.length; i++) {
    var p = particles[i];
    if (p.life === 0) {
      particles.splice(i, 1);
      var p = new Particle();
      particles.push(p);
    }

    p.update();

    if (p.m > 0) {
      ctx.save();
      ctx.globalAlpha = p.op;
      ctx.fillStyle = p.color + p.op + ")";
      ctx.beginPath();
      ctx.arc(p.x * p.m + CenterX, CenterY - p.y * p.m, p.radius * p.m, 0, Math.PI * 2);
      ctx.fill();
      ctx.restore();
    }
  }
  animationId = requestAnimationFrame(loop);
}

function initCanvas() {
  width = canvas.width = window.innerWidth;
  height = canvas.height = window.innerHeight;
  CenterX = width / 2;
  CenterY = height / 2;
}

export default {
  data() {
    return {}
  },
  mounted() {
    console.log('Renderjs mounted')
    this.initCanvas()
  },
  methods: {
    initCanvas() {
      console.log('initCanvas started')
      
      canvas = document.createElement('canvas')
      const container = document.querySelector('.container')
      
      ctx = canvas.getContext("2d")
      
      if (container) {
        container.appendChild(canvas)
        container.style.margin = "0"
        container.style.padding = "0"
        container.style.overflow = "hidden"
        container.style.width = "100%"
        container.style.height = "100%"
        container.style.background = OPT.backgroundColor
      }
      
      initCanvas()
      loop()
      console.log('Animation loop started')
    }
  },
  beforeDestroy() {
    if (animationId) {
      cancelAnimationFrame(animationId)
    }
  }
}
</script>

<style>
.container {
	width: 100vw;
	height: 100vh;
	overflow: hidden;
	margin: 0;
	background: #212020;
	position: relative;
}


.add_shadow{
      box-shadow: 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white);
}

.login-wrapper {
	position: absolute;
	top: 80rpx;
	left: 0;
	right: 0;
	display: flex;
	justify-content: center;
	z-index: 100;
}

.login-box {
	width: 600rpx;
	/* background: rgba(0, 0, 0, 0.1); */
	/* backdrop-filter: blur(20px); */
	border-radius: 32rpx;
	padding: 60rpx 40rpx;
	/* border: 1rpx solid rgba(255, 255, 255, 0.1); */
	/* box-shadow: 0 20rpx 60rpx rgba(0, 0, 0, 0.5); */
    /* box-shadow: 6rpx 6rpx 12rpx var(--greyLight-2), -4rpx -4rpx 10rpx var(--white); */
}

.login-title {
	font-size: 38rpx;
	color: rgba(255, 255, 255, 0.7);
	font-weight: bold;
	text-align: center;
	display: block;
	margin-bottom: 30rpx;
	letter-spacing: 8rpx;
}

.input-group {
	display: flex;
	flex-direction: column;
	gap: 20rpx;
}

.input-item {
	background: rgba(255, 255, 255, 0.1);
	border-radius: 40rpx;
	border: 1rpx solid rgba(255, 255, 255, 0.2);
	padding: 0 30rpx;
}

.input-item input {
	width: 100%;
	height: 68rpx;
	background: transparent;
	font-size: 28rpx;
	color: #fff;
}

.input-placeholder {
	color: rgba(255, 255, 255, 0.5);
}

.login-btn {
	/* width: 100%; */
	/* height: 68rpx; */
	display: flex;
	justify-content: center;
	align-items: center;
	/* background: linear-gradient(45deg, #ff357a, #fff172); */
	background: linear-gradient(120deg, #07c160, #34fc6a);
	border-radius: 40rpx;
	margin-top: 30rpx;
    padding: 16rpx 32rpx;
}

.btn-text {
	font-size: 28rpx;
	color: rgba(255, 255, 255, 0.8);
	font-weight: bold;
	letter-spacing: 8rpx;
}

.links {
    position: absolute;
    left: 0;
    bottom: 81px;
    /* border: #fff172 solid 1px; */
    box-sizing: border-box;
    width: 100vw;
	display: flex;
	justify-content: space-between;
	padding: 0 81rpx;
}

.link-text {
	font-size: 28rpx;
	color: rgba(255, 255, 255, 0.7);
}
</style>