<template>
	<view class="avatar-container" :style="containerStyle">
		<view class="avatar-text-wrapper">
			<text
				v-for="(line, index) in lines"
				:key="index"
				class="avatar-line"
				:style="lineStyle"
			>{{ line }}</text>
		</view>
	</view>
</template>

<script>
// ============================================================
// 1. 工具函数：HSL → HEX（用于自动生成双色渐变 21种，保留原逻辑）
// ============================================================
function hslToHex(h, s, l) {
	h = ((h % 360) + 360) % 360;
	s = Math.min(100, Math.max(0, s));
	l = Math.min(100, Math.max(0, l));
	const c = (1 - Math.abs(2 * l / 100 - 1)) * (s / 100);
	const x = c * (1 - Math.abs((h / 60) % 2 - 1));
	const m = l / 100 - c / 2;
	let r, g, b;
	if (h < 60) { r = c; g = x; b = 0; }
	else if (h < 120) { r = x; g = c; b = 0; }
	else if (h < 180) { r = 0; g = c; b = x; }
	else if (h < 240) { r = 0; g = x; b = c; }
	else if (h < 300) { r = x; g = 0; b = c; }
	else { r = c; g = 0; b = x; }
	const toHex = (v) => Math.round((v + m) * 255).toString(16).padStart(2, '0');
	return `#${toHex(r)}${toHex(g)}${toHex(b)}`;
}

// ============================================================
// 2. 内置单色背景（21 种，原有不变）
// ============================================================
const SINGLE_COLORS = [
	'#ffb34b', '#f2bba9', '#f7a196', '#f18080', '#2fe25f',
	'#07c160', '#0eb805', '#94d554', '#f19ec2', '#afaae4',
	'#e1b0df', '#c38cc1', '#72dcdc',  '#aa00ff', '#0caaff',
	'#48d3f9', '#86cefa', '#98d1ee',  '#f5cc00', '#d9534f',
	'#ff55ff'
];

// ============================================================
// 3.1 原有自动生成双色渐变（21种，保留）
// ============================================================
const generateDualGradients = (count = 21) => {
	const gradients = [];
	const hueStep = 360 / count;
	for (let i = 0; i < count; i++) {
		const hue1 = i * hueStep;
		const hue2 = (hue1 + 60) % 360;
		gradients.push([
			hslToHex(hue1, 80, 60),
			hslToHex(hue2, 80, 60)
		]);
	}
	return gradients;
};
const AUTO_DUAL_GRADIENTS = generateDualGradients(21);

// ============================================================
// 3.2 【新增】手工精选双色渐变 30组（莫兰迪/马卡龙/商务/治愈）
// ============================================================
const CUSTOM_DUAL_GRADIENTS = [
	// 莫兰迪低饱和
	['#d4a5a5', '#e6d4d4'],
	['#e29fef', '#d0d0e0'],
	['#e6c8b4', '#f2e0d4'],
	// 马卡龙清新
	['#f8a5eb', '#ffecf2'],
	['#a1d3f0', '#e0f0ff'],
	['#95ea98', '#e8fff0'],
	['#f8d927', '#fffbe0'],
	['#f5b7ff', '#f2e6ff'],
	// 日落暖调
	['#ffb6b9', '#fae3d9'],
	['#eebe6a', '#ffefc7'],
	['#ff9a8b', '#ff6a88'],
	['#f6d365', '#fda085'],
	['#ffc371', '#ff5f6d'],
	// 冷调清爽 55
	['#4facfe', '#00f2fe'],
	['#43e97b', '#38f9d7'],
	['#6f89ff', '#b676ff'], 
	['#37eeee', '#7912f7'],
	['#5ee7df', '#e06bea'],
	// 商务高级深色 60
	['#0055ff', '#64d6e7'],
	['#0f3443', '#34e89e'],
	['#1a2980', '#26d0ce'],
	['#232526', '#ff1de9'],
	['#ff1de9', '#fecfef'],
	// 温柔粉紫
	['#f093fb', '#f5576c'],
	['#a18cd1', '#fbc2eb'],
	['#c471ed', '#f64f59'],
	['#eb596f', '#ffdde1'],
	['#de80dd', '#fef9d7']
];

// 合并全部双色渐变 = 自动生成21 + 手工新增28
const ALL_DUAL_GRADIENTS = [...AUTO_DUAL_GRADIENTS, ...CUSTOM_DUAL_GRADIENTS];

// ============================================================
// 4.1 原有手工三色渐变（21种，保留不变）
// ============================================================
const OLD_TRI_GRADIENTS = [
    // 73
	['#f093fb', '#f5576c', '#4facfe'],
	['#43e97b', '#38f9d7', '#fa709a'],
	['#fa709a', '#fee140', '#f6d365'],
	['#a18cd1', '#fbc2eb', '#f6d365'],
	['#fccb90', '#d57eeb', '#f6d365'],
	['#ffecd2', '#fcb69f', '#ff9a9e'],
	['#a1c4fd', '#c2e9fb', '#fbc2eb'],
    //80
	['#fbc2eb', '#a6c1ee', '#f6d365'],
	['#f6d365', '#fda085', '#fbc2eb'],
	['#a18cd1', '#fda085', '#f6d365'],
	['#ff9a9e', '#fecfef', '#f6d365'],
	['#ffecd2', '#fcb69f', '#a1c4fd'],
	['#a18cd1', '#fbc2eb', '#c2e9fb'],
	['#f093fb', '#f5576c', '#a1c4fd'],
	['#43e97b', '#38f9d7', '#f6d365'],
	['#fa709a', '#fee140', '#fbc2eb'],
	['#fccb90', '#d57eeb', '#a6c1ee'],
	['#ffecd2', '#fcb69f', '#4facfe'],
	['#a18cd1', '#fbc2eb', '#fda085'],
	['#f6d365', '#fda085', '#fecfef'],
	['#f093fb', '#f5576c', '#f6d365']
];

// ============================================================
// 4.2 【新增】高级三色渐变 35组（治愈/日落/森系/国风/ins梦幻）
// ============================================================
const CUSTOM_TRI_GRADIENTS = [
	// 马卡龙治愈浅系 94
	[ '#a1c4fd', '#c6e5ff' , '#e0f7ff'],
	[ '#e8cd5e', '#ffd993' , '#fef9e7'],
	[ '#9be15d' , '#bfe6c8' , '#e8fff0'],
	['#fce4f7', '#f0c6e8', '#e1b0df'],
	[ '#dce7ff', '#b8b8d0', '#f0f4ff'],
	// 日落晚霞橙红 99
	['#fad0c4' , '#ff9a9e', '#f6d365'],
	['#ff758c', '#ff7eb3', '#ffd89b'],
	['#f6d365', '#fda085', '#ff9a8b'],
	['#ffecd2', '#fcb69f', '#ff8a80'],
	['#f5af19', '#f12711', '#ff9a9e'],
	// 森系青绿色 104
	['#38ef7d', '#11998e', '#43e97b'],
	['#76d7c4', '#48c9b0', '#1abc9c'],
	['#a8e063', '#56ab2f', '#38f9d7'],
	['#c4e538', '#00b09b', '#96c93d'],
	['#5ee7df', '#d4aaee', '#43e97b'],
	// 梦幻蓝紫ins风 109
	['#667eea', '#764ba2', '#f093fb'],
	['#4facfe', '#00f2fe', '#a18cd1'],
	['#c471ed', '#f64f59', '#a6c1ee'],
	['#7b4397', '#dc2430', '#fbc2eb'],
	['#30cfd0', '#7a12f9', '#d299c2'],
	// 商务低饱和深色 114
	['#2c3e50', '#4ca1af', '#00c6fb'],
    [ '#e37682' , '#aa00ff', '#35c9fd'],
	// ['#141e30', '#8100c2', '#38c3fa'],
	['#1a2980', '#26d0ce', '#00d2ff'],
    ['#35c9fd' , '#e42fef', '#e37682'],
	['#aa00ff', '#f475ff', '#ffaa00'],
	// 国风淡雅古风 119
	['#f8c8d0', '#e8d0e8', '#d0e0f0'],
	['#f2e8d0', '#e0e8d0', '#d0d8d0'],
	['#e8e0f0', '#d8d0e8', '#c8c8e0'],
	['#f0d8d0', '#e8c8c8', '#d8c8d8'],
	['#e0f0e8', '#c8e8e0', '#b8c8d0'],
	// 温柔蜜桃豆沙
	['#ffd6e0', '#f8c8d0', '#f2b8c8'],
	['#fae3d9', '#ffc3b8', '#ffb6b9'],
	['#fee1e8', '#fccbcf', '#f8a8b8'],
	['#ffdde1', '#ee9ca7', '#f6c8d0'],
	['#fef0f4', '#f8d8e0', '#f0c8d8']
];

// 合并全部三色渐变 = 原有21 + 新增35
const ALL_TRI_GRADIENTS = [...OLD_TRI_GRADIENTS, ...CUSTOM_TRI_GRADIENTS];

// ============================================================
// 5. 合并所有预设（单色 → 全部双色 → 全部三色）
// 索引分段说明：
// 0~20    SINGLE_COLORS 22个单色
// 21~69   ALL_DUAL_GRADIENTS 51组双色(21自动+30手工)
// 70~125  ALL_TRI_GRADIENTS 56组三色(21旧+35新增)
// ============================================================
const PRESET_LIST = [
	...SINGLE_COLORS,
	...ALL_DUAL_GRADIENTS,
	...ALL_TRI_GRADIENTS
];

// ============================================================
// 6. 组件定义（原有逻辑完全不变，无需改动）
// ============================================================
export default {
	name: 'aye-avatar',
	props: {
		size: {
			type: [Number, String],
			default: 36
		},
		fontSize: {
			type: Number,
			default: null
		},
		color: {
			type: String,
			default: '#ffffff'
		},
		bgColor: {
			type: String,
			default: '#07c160'
		},
		gradientColors: {
			type: [Array, String],
			default: () => []
		},
		gradientAngle: {
			type: [Number, String],
			default: 120
		},
		text: {
			type: String,
			default: ''
		},
		shape: {
			type: String,
			default: 'square',
			validator: (val) => ['round', 'square'].includes(val)
		},
		autoFontSize: {
			type: Boolean,
			default: true
		},
		shadow: {
			type: String,
			default: '3px 3px 6px #c8d0e7, -1px -1px 1px rgba(255, 255, 255, 0.9)'
		},
		bgColorIndex: {
			type: Number,
			default: null
		},
		randomBgColor: {
			type: Boolean,
			default: false
		}
	},
	data() {
		return {
			randomPreset: null
		};
	},
	created() {
		if (this.randomBgColor) {
			this.randomPreset = Math.floor(Math.random() * PRESET_LIST.length);
		}
	},
	computed: {
		// ---------- 换行逻辑 ----------
		lines() {
			const raw = this.text || '?';
			const chars = raw.slice(0, 9).split('');
			const total = chars.length;
			if (total === 0) return ['?'];

			let rows = 1;
			if (total >= 4 && total <= 6) rows = 2;
			if (total >= 7) rows = 3;

			const base = Math.floor(total / rows);
			let remain = total % rows;
			const perRow = [];
			for (let i = 0; i < rows; i++) {
				let count = base + (remain > 0 ? 1 : 0);
				if (count > 3) count = 3;
				if (count <= 0) count = 1;
				perRow.push(count);
				if (remain > 0) remain--;
			}
			let idx = 0;
			const linesArr = [];
			for (let i = 0; i < rows; i++) {
				const end = Math.min(idx + perRow[i], total);
				const line = chars.slice(idx, end).join('');
				linesArr.push(line);
				idx = end;
			}
			return linesArr.filter(line => line.length > 0);
		},
		charCount() {
			return this.text ? this.text.slice(0, 9).length : 0;
		},

		// ---------- 字体大小计算（优化后） ----------
		computedFontSize() {
			if (this.fontSize !== null && this.fontSize > 0) {
				return this.fontSize;
			}
			if (!this.autoFontSize) {
				return this.size * 0.35;
			}
			const size = Number(this.size) || 36;
			const count = this.charCount;
			if (count === 0) return 14;

			const size36Map = {
				1: 14, 2: 12, 3: 10, 4: 10, 5: 9, 6: 9, 7: 8, 8: 8, 9: 8
			};
			if (size === 36 && count in size36Map) {
				return size36Map[count];
			}

			const available = size * 0.92;

			let fontSize;
			if (count === 1) {
				fontSize = available / 2;
			} else if (count === 2) {
				fontSize = available / 2 * 0.8;
			} else if (count >= 3 && count <= 6) {
				fontSize = available / 3 * 0.8;
			} else {
				fontSize = available / (3 * 1.2);
			}
			return Math.round(fontSize * 10) / 10;
		},

		// ---------- 解析自定义渐变色 ----------
		parsedGradientColors() {
			let colors = this.gradientColors;
			if (typeof colors === 'string') {
				try {
					colors = JSON.parse(colors.replace(/'/g, '"'));
				} catch (e) {
					colors = [];
				}
			}
			return Array.isArray(colors) ? colors : [];
		},
		parsedAngle() {
			const angle = Number(this.gradientAngle);
			return isNaN(angle) ? 120 : angle;
		},

		// ---------- 获取预设背景（单色或渐变） ----------
		presetBackground() {
			const idx = this.randomBgColor ? this.randomPreset : this.bgColorIndex;
			if (idx === null || idx === undefined || isNaN(idx)) return null;
			const num = Number(idx);
			if (!Number.isInteger(num) || num < 0 || num >= PRESET_LIST.length) return null;
			return PRESET_LIST[num];
		},

		// ---------- 最终背景样式 ----------
		backgroundStyle() {
			const preset = this.presetBackground;

			if (preset !== null) {
				if (typeof preset === 'string') {
					return { backgroundColor: preset };
				}
				if (Array.isArray(preset) && preset.length >= 2) {
					return {
						backgroundImage: `linear-gradient(${this.parsedAngle}deg, ${preset.join(', ')})`
					};
				}
			}

			const customColors = this.parsedGradientColors;
			if (customColors && customColors.length >= 2) {
				return {
					backgroundImage: `linear-gradient(${this.parsedAngle}deg, ${customColors.join(', ')})`
				};
			}
			return { backgroundColor: this.bgColor || '#1890ff' };
		},

		// ---------- 容器样式 ----------
		containerStyle() {
			const size = Number(this.size) || 36;
			const isRound = this.shape === 'round';
			// const shadowStyle = this.shadow ? {
				// boxShadow: '3px 3px 6px #c8d0e7, -1px -1px 1px rgba(255, 255, 255, 0.9)'
			// } : {};
			return {
				// ...shadowStyle,
                boxShadow: this.shadow ,
				width: size + 'px',
				height: size + 'px',
				borderRadius: isRound ? '50%' : (size * 0.2 + 'px'),
				...this.backgroundStyle,
				overflow: 'hidden',
				display: 'flex',
				justifyContent: 'center',
				alignItems: 'center',
				userSelect: 'none',
				WebkitUserSelect: 'none'
			};
		},

		lineStyle() {
			return {
				color: this.color || '#ffffff',
				fontSize: this.computedFontSize + 'px',
				fontWeight: '500',
				lineHeight: 1.2,
				textAlign: 'center',
				whiteSpace: 'nowrap',
				textShadow: '0 1px 4px rgba(0,0,0,0.12)'
			};
		}
	}
};
</script>

<style scoped>
.avatar-container {
	flex-shrink: 0;
}
.avatar-text-wrapper {
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
	width: 100%;
	height: 100%;
	padding: 4% 4%;
	box-sizing: border-box;
}
.avatar-line {
	display: block;
	width: 100%;
	text-align: center;
	user-select: none;
	-webkit-user-select: none;
}
</style>