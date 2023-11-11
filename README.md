# lottey
体彩彩票排列三,排列3彩票源码

部署教程和源码备份下载地址
链接：https://pan.baidu.com/s/1gWQckRKM-pY7uCiujZB54g?pwd=4bf7 
提取码：4bf7

仿中国体育擦彩票排列三源码
前端代码如下：
<template>
	<view class="box">

		<cmd-nav-bar back title="排列3" font-color="#fff" background-color="#FF3F43" right-text="排列3开奖"
			@rightText="rightBtn">
		</cmd-nav-bar>
		<div style="height:100%">
			<u-subsection style="margin-top: 2px;height: 40px;" fontSize="16" :list="list" mode="button"
				:current="current" activeColor="#FF3F43" @change="change3"></u-subsection>
			<p class="fc_index">第{{issueNo}}期，21:40开奖</p>
			<view v-if="current==0">
				<u-sticky bgColor="#fff"
					style="margin-bottom: 30px;display: flex;justify-content: center;align-items: center;">
					<u-tabs :list="tabs" lineColor="#FF3F43"
						:activeStyle="{color: '#FF3F43',fontWeight: 'bold',transform: 'scale(1.05)'}"
						@click="changeSelectBall($event,1)" :current="zindex"></u-tabs>
				</u-sticky>
				<div class="fc" v-if="zindex==0">
					<view
						style="display: flex;justify-content: space-between;align-items: center;width: 95%;margin: 0 auto;">
						<p class="tips"><span class="shake"></span>选择<span>3</span>个号码，中奖<span>1040</span>元</p>
						<u-checkbox-group @change="checkChange" size="15" shape="square" placement="column"
							style="margin-left: 20px;">
							<u-checkbox labelSize="14" activeColor="#FF3F43" :label="'显示遗漏'">
							</u-checkbox>
						</u-checkbox-group>
					</view>
					<ul>
						<p>百位</p>
						<li @click="check(1,1,index)" v-for="(item,index) in bai" :class="item.active?'active':''">
							{{item.num}}
							<view v-if="omitData.record!=undefined&&omiIsShow"
								style="color: #A5A5A5;font-size: 13px;margin-top: -8px;">
								{{omitData.record[index]}}
							</view>
						</li>
					</ul>
					<u-divider></u-divider>
					<ul>
						<p>十位</p>
						<li @click="check(1,2,index)" v-for="(item,index) in shi" :class="item.active?'active':''">
							{{item.num}}
							<view v-if="omitData.record!=undefined&&omiIsShow"
								style="color: #A5A5A5;font-size: 13px;margin-top: -8px;">
								{{omitData.record[index+10]}}
							</view>
						</li>
					</ul>
					<u-divider></u-divider>
					<ul>
						<p>个位</p>
						<li @click="check(1,3,index)" v-for="(item,index) in ge" :class="item.active?'active':''">
							{{item.num}}
							<view v-if="omitData.record!=undefined&&omiIsShow"
								style="color: #A5A5A5;font-size: 13px;margin-top: -8px;">
								{{omitData.record[index+20]}}
							</view>
						</li>
					</ul>
				</div>
				<div class="fc" v-else-if="zindex==1">
					<p class="tips"><span class="shake"></span>选择<span>1</span>个号码，中奖<span>1040</span>元</p>
					<ul>
						<li @click="check(2,1,index)" v-for="(item,index) in directlyElectedGentle"
							:class="item.active?'active':''">
							{{item.num}}
						</li>
					</ul>
				</div>
			</view>
			<view v-if="current==1">
				<u-sticky bgColor="#fff"
					style="margin-bottom: 30px;display: flex;justify-content: center;align-items: center;">
					<u-tabs :list="tabs1" lineColor="#FF3F43"
						:activeStyle="{color: '#FF3F43',fontWeight: 'bold',transform: 'scale(1.05)'}"
						@click="changeSelectBall($event,2)" :current="zindex"></u-tabs>
				</u-sticky>
				<div class="fc" v-if="zindex==0">
					<p class="tips"><span class="shake"></span>至少选择<span>2</span>个号码，中奖<span>346</span>元</p>
					<ul>
						<p>选号</p>
						<li @click="check(3,1,index)" v-for="(item,index) in san" :class="item.active?'active':''">
							{{item.num}}<span style="font-size: 15px;" v-if="item.isGallbladder">胆</span>
							<u-checkbox-group shape="square" @change="checkboxChange($event,index,1)"
								:disabled="redLength>=1&&item.isGallbladder==false">
								<u-checkbox activeColor="#FF3F43" :name="item.isGallbladder"
									:checked="item.isGallbladder">
								</u-checkbox>
							</u-checkbox-group>
						</li>
					</ul>
				</div>
				<div class="fc" v-if="zindex==1">
					<p class="tips"><span class="shake"></span>至少选择<span>3</span>个号码，中奖<span>173</span>元</p>
					<ul>
						<p>选号</p>
						<li @click="check(4,2,index)" v-for="(item,index) in liu" :class="item.active?'active':''">
							{{item.num}}<span style="font-size: 15px;" v-if="item.isGallbladder">胆</span>
							<u-checkbox-group shape="square" @change="checkboxChange($event,index,2)"
								:disabled="blueLength>=2&&item.isGallbladder==false">
								<u-checkbox activeColor="#FF3F43" :name="item.isGallbladder"
									:checked="item.isGallbladder">
								</u-checkbox>
							</u-checkbox-group>
						</li>
					</ul>
				</div>
				<div class="fc" v-else-if="zindex==2">
					<p class="tips"><span class="shake"></span>组三中奖<span>346</span>元，组六中奖<span>173</span>元</p>
					<ul>
						<li @click="check(5,0,index)" v-for="(item,index) in groupGentle"
							:class="item.active?'active':''">
							{{item.num}}
						</li>
					</ul>
				</div>
				<div class="fc" v-else-if="zindex==3">
					<ul>
						<p>对子</p>
						<li @click="check(6,1,index)" v-for="(item,index) in shi" :class="item.active?'active':''">
							{{item.num}}
						</li>
					</ul>
					<u-divider></u-divider>
					<ul>
						<p>非对子</p>
						<li @click="check(6,2,index)" v-for="(item,index) in ge" :class="item.active?'active':''">
							{{item.num}}
						</li>
					</ul>
					<u-divider></u-divider>
					<view style="font-size: 12px;width: 90%;margin: auto;margin-top: 30px;color: #868686;">
						<p>示例</p>
						<p>对子号码选择0，非对子号码选择1，则组三单式号码为001</p>
						<p>对子号码选择0和1，非对子号码选择2，则组三单式号码为002、112</p>
					</view>
				</div>
			</view>
			<Acount :total="total" :acount="acount" @clear="clear" @confirm="sure" />
		</div>

	</view>
</template>
<script>
	import {
		getIssueNo
	} from '@/api/pailie.js'
	import {
		getOmitByType
	} from '@/api/omit.js'
	import Acount from '../common/Acount'
	export default {
		data() {
			return {
				//胆1的长度
				redLength: 0,
				//胆2的长度
				blueLength: 0,
				//当前选择的索引
				zindex: 0,
				list: ['直选', '组选'],
				current: 0,
				total: 0,
				acount: 0,
				issueNo: "",
				//tab1选项
				tabs: [{
					name: '直选',
				}, {
					name: '和值',
				}],
				//tab2选项
				tabs1: [{
					name: '组三',
				}, {
					name: '组六',
				}, {
					name: '和值',
				}, {
					name: '组三单式',
				}],
				//直选和值
				directlyElectedGentle: [{
						num: 0,
						active: false,
						pour: 1
					}, {
						num: 1,
						active: false,
						pour: 3
					}, {
						num: 2,
						active: false,
						pour: 6
					}, {
						num: 3,
						active: false,
						pour: 10
					}, {
						num: 4,
						active: false,
						pour: 15
					},
					{
						num: 5,
						active: false,
						pour: 21
					}, {
						num: 6,
						active: false,
						pour: 28
					}, {
						num: 7,
						active: false,
						pour: 36
					}, {
						num: 8,
						active: false,
						pour: 45
					}, {
						num: 9,
						active: false,
						pour: 55
					}, {
						num: 10,
						active: false,
						pour: 63
					}, {
						num: 11,
						active: false,
						pour: 69
					}, {
						num: 12,
						active: false,
						pour: 73
					}, {
						num: 13,
						active: false,
						pour: 75
					}, {
						num: 14,
						active: false,
						pour: 75
					}, {
						num: 15,
						active: false,
						pour: 73
					}, {
						num: 16,
						active: false,
						pour: 69
					}, {
						num: 17,
						active: false,
						pour: 63
					}, {
						num: 18,
						active: false,
						pour: 55
					}, {
						num: 19,
						active: false,
						pour: 45
					}, {
						num: 20,
						active: false,
						pour: 36
					}, {
						num: 21,
						active: false,
						pour: 28
					}, {
						num: 22,
						active: false,
						pour: 21
					}, {
						num: 23,
						active: false,
						pour: 15
					}, {
						num: 24,
						active: false,
						pour: 10
					}, {
						num: 25,
						active: false,
						pour: 6
					}, {
						num: 26,
						active: false,
						pour: 3
					}, {
						num: 27,
						active: false,
						pour: 1
					}
				],
				groupGentle: [{
						num: 1,
						active: false,
						pour: 1
					}, {
						num: 2,
						active: false,
						pour: 2
					}, {
						num: 3,
						active: false,
						pour: 2
					}, {
						num: 4,
						active: false,
						pour: 4
					},
					{
						num: 5,
						active: false,
						pour: 5
					}, {
						num: 6,
						active: false,
						pour: 6
					}, {
						num: 7,
						active: false,
						pour: 8
					}, {
						num: 8,
						active: false,
						pour: 10
					}, {
						num: 9,
						active: false,
						pour: 11
					}, {
						num: 10,
						active: false,
						pour: 13
					}, {
						num: 11,
						active: false,
						pour: 14
					}, {
						num: 12,
						active: false,
						pour: 14
					}, {
						num: 13,
						active: false,
						pour: 15
					}, {
						num: 14,
						active: false,
						pour: 15
					}, {
						num: 15,
						active: false,
						pour: 14
					}, {
						num: 16,
						active: false,
						pour: 14
					}, {
						num: 17,
						active: false,
						pour: 13
					}, {
						num: 18,
						active: false,
						pour: 11
					}, {
						num: 19,
						active: false,
						pour: 10
					}, {
						num: 20,
						active: false,
						pour: 8
					}, {
						num: 21,
						active: false,
						pour: 6
					}, {
						num: 22,
						active: false,
						pour: 5
					}, {
						num: 23,
						active: false,
						pour: 4
					}, {
						num: 24,
						active: false,
						pour: 2
					}, {
						num: 25,
						active: false,
						pour: 2
					}, {
						num: 26,
						active: false,
						pour: 1
					}
				],

				ge: [{
						num: 0,
						active: false
					}, {
						num: 1,
						active: false
					}, {
						num: 2,
						active: false
					}, {
						num: 3,
						active: false
					}, {
						num: 4,
						active: false
					},
					{
						num: 5,
						active: false
					}, {
						num: 6,
						active: false
					}, {
						num: 7,
						active: false
					}, {
						num: 8,
						active: false
					}, {
						num: 9,
						active: false
					}
				],
				shi: [{
						num: 0,
						active: false
					}, {
						num: 1,
						active: false
					}, {
						num: 2,
						active: false
					}, {
						num: 3,
						active: false
					}, {
						num: 4,
						active: false
					},
					{
						num: 5,
						active: false
					}, {
						num: 6,
						active: false
					}, {
						num: 7,
						active: false
					}, {
						num: 8,
						active: false
					}, {
						num: 9,
						active: false
					}
				],
				bai: [{
						num: 0,
						active: false
					}, {
						num: 1,
						active: false
					}, {
						num: 2,
						active: false
					}, {
						num: 3,
						active: false
					}, {
						num: 4,
						active: false
					},
					{
						num: 5,
						active: false
					}, {
						num: 6,
						active: false
					}, {
						num: 7,
						active: false
					}, {
						num: 8,
						active: false
					}, {
						num: 9,
						active: false
					}
				],
				san: [{
						num: 0,
						active: false,
						isGallbladder: false
					}, {
						num: 1,
						active: false,
						isGallbladder: false
					}, {
						num: 2,
						active: false,
						isGallbladder: false
					}, {
						num: 3,
						active: false,
						isGallbladder: false
					}, {
						num: 4,
						active: false,
						isGallbladder: false
					},
					{
						num: 5,
						active: false,
						isGallbladder: false
					}, {
						num: 6,
						active: false,
						isGallbladder: false
					}, {
						num: 7,
						active: false,
						isGallbladder: false
					}, {
						num: 8,
						active: false,
						isGallbladder: false
					}, {
						num: 9,
						active: false,
						isGallbladder: false
					}
				],
				liu: [{
						num: 0,
						active: false,
						isGallbladder: false
					}, {
						num: 1,
						active: false,
						isGallbladder: false
					}, {
						num: 2,
						active: false,
						isGallbladder: false
					}, {
						num: 3,
						active: false,
						isGallbladder: false
					}, {
						num: 4,
						active: false,
						isGallbladder: false
					},
					{
						num: 5,
						active: false,
						isGallbladder: false
					}, {
						num: 6,
						active: false,
						isGallbladder: false
					}, {
						num: 7,
						active: false,
						isGallbladder: false
					}, {
						num: 8,
						active: false,
						isGallbladder: false
					}, {
						num: 9,
						active: false,
						isGallbladder: false
					}
				],
				gearr: [],
				shiarr: [],
				baiarr: [],
				sanarr: [],
				liuarr: [],
				directlyElectedGentleArr: [],
				groupGentleArr: [],
				omitData: {},
				omiIsShow: false,
			}
		},
		components: {
			Acount
		},
		onLoad() {
			this.init()
		},
		methods: {
			checkChange(item) {
				if (item[0] == "") {
					this.omiIsShow = true;
				} else {
					this.omiIsShow = false;
				}
			},
			checkboxChange(item, index, type) {
				if (type == 1) {
					this.san[index].isGallbladder = !this.san[index].isGallbladder;
					this.gallbladderStatistics(type);
				} else if (type == 2) {
					this.liu[index].isGallbladder = !this.liu[index].isGallbladder;
					this.gallbladderStatistics(type);
				}
				if (item[0] != undefined) {
					if (type == 1) {
						this.san[index].active = true;
					} else if (type == 2) {
						this.liu[index].active = true;
					}
				}
				if (type == 1) {
					this.sanarr = this.san.filter(v => {
						return v.active
					})
				} else if (type == 2) {
					this.liuarr = this.liu.filter(v => {
						return v.active
					})
				}
				this.calculate(type)
			},
			calculate(type) {
				//1 组三 2组六
				if (type == 1) {
					//选择二个或者以上才进行判断
					if (this.sanarr.length > 1) {
						//是否选了胆
						let flag = false;
						//选中的胆的数字
						let dan = "";
						this.sanarr.map(item => {
							//判断是否选中了胆
							if (item.isGallbladder) {
								flag = true;
								dan = item.num
							}
						})
						//没有选中胆直接用原来计算注的
						if (flag) {
							let list = [];
							for (let i = 0; i < this.sanarr.length; i++) {
								for (let j = i + 1; j < this.sanarr.length; j++) {
									let a = this.sanarr[i].num;
									let b = this.sanarr[j].num;
									//过滤掉不是胆的组合
									if (a != dan && b != dan) {
										continue;
									}
									list.push(a + "," + a + "," + b);
									list.push(a + "," + b + "," + a);
									list.push(a + "," + b + "," + b);
									list.push(b + "," + a + "," + b);
									list.push(b + "," + b + "," + a);
									list.push(b + "," + a + "," + a);
								}
							}
							//一注是三组 所以除了3就是得到的所有注数
							this.acount = list.length / 3
						} else {
							this.acount = this.globalUtil.math(this.sanarr.length, 2) * 2;
						}
						//计算金额
						this.total = this.acount * 2;
					} else {
						this.total = 0;
						this.acount = 0;
					}
				} else {
					//选择二个或者以上才进行判断
					if (this.liu.length > 2) {
						//是否选了胆
						let flag = false;
						//选中的胆的数字
						let danArr = [];
						this.liuarr.map(item => {
							//判断是否选中了胆
							if (item.isGallbladder) {
								flag = true;
								danArr.push(item.num)
							}
						})
						//没有选中胆直接用原来计算注的
						if (flag) {
							let list = [];
							for (let i = 0; i < this.liuarr.length; i++) {
								for (let j = 0; j < this.liuarr.length; j++) {
									for (let k = 0; k < this.liuarr.length; k++) {
										if (this.liuarr[i].num != this.liuarr[j].num && this.liuarr[j].num != this.liuarr[
												k].num && this
											.liuarr[i].num != this.liuarr[k].num) {
											//添加组合
											list.push(this.liuarr[i].num + "," + this.liuarr[j].num + "," + this.liuarr[k]
												.num)
										}
									}
								}
							}
							//过滤胆
							list = list.filter(item => {
								if (danArr.length == 1) {
									return item.includes(danArr[0]);
								} else {
									return item.includes(danArr[0]) && item.includes(danArr[1]);
								}
							})
							//一注是三组 所以除了6就是得到的所有注数
							this.acount = list.length / 6
						} else {
							this.acount = this.globalUtil.math(this.liuarr.length, 3);
						}
						//计算金额
						this.total = this.acount * 2;
					} else {
						this.total = 0;
						this.acount = 0;
					}
				}
			},
			gallbladderStatistics(type) {
				if (type == 1) {
					let s1 = this.san.filter(item => {
						return item.isGallbladder;
					})
					this.redLength = s1.length
				} else if (type == 2) {
					let s2 = this.liu.filter(item => {
						return item.isGallbladder;
					})
					this.blueLength = s2.length
				}
			},
			//切换事件
			change3(index) {
				let data = uni.getStorageSync('pailie');
				if (data != "") {
					uni.showModal({
						title: '玩家切换提醒',
						content: '不支持直选和组选的混合投注，切换玩法将清空已选择号码，是否仍要切换',
						success: (res => {
							if (res.confirm) {
								uni.removeStorageSync("pailie")
								this.current = index
								this.zindex = 0;
								this.clear();
							}
						}),
					});
				} else {
					this.current = index
					this.zindex = 0;
					this.clear();
				}
			},
			init() {
				getIssueNo("3").then(res => {
					this.issueNo = res.stageNumber
				})
				getOmitByType("3").then(res => {
					this.omitData = res
					this.omitData.record = res.record.split(",")
				})
			},
			rightBtn() {
				uni.navigateTo({
					url: "/pages/pailie/openPrize"
				})
			},
			check(type, wei = 0, index) {
				switch (type) {
					case 1:
						if (wei == 1) {
							this.bai[index].active = !this.bai[index].active;
						};
						if (wei == 2) {
							this.shi[index].active = !this.shi[index].active;
						};
						if (wei == 3) {
							this.ge[index].active = !this.ge[index].active;
						};
						this.shiarr = this.shi.filter(v => {
							return v.active
						})
						this.baiarr = this.bai.filter(v => {
							return v.active
						})
						this.gearr = this.ge.filter(v => {
							return v.active
						})
						this.acount = this.globalUtil.math(this.baiarr.length, 1) * this.globalUtil.math(this.shiarr
							.length, 1) * this.globalUtil.math(this.gearr.length, 1)
						break;
					case 2:
						this.directlyElectedGentle[index].active = !this.directlyElectedGentle[index].active;
						this.directlyElectedGentleArr = this.directlyElectedGentle.filter(v => {
							return v.active
						});
						let count = 0;
						this.directlyElectedGentleArr.map(item => {
							if (item.active) {
								count += item.pour
							}
						})
						this.acount = count;
						break;
					case 3:
						this.san[index].active = !this.san[index].active;
						this.san[index].isGallbladder = false;
						this.gallbladderStatistics(wei)
						this.sanarr = this.san.filter(v => {
							return v.active
						});
						this.calculate(wei)
						break;
					case 4:
						this.liu[index].active = !this.liu[index].active;
						this.liu[index].isGallbladder = false;
						this.gallbladderStatistics(wei)
						this.liuarr = this.liu.filter(v => {
							return v.active
						});
						this.calculate(wei)
						break;
					case 5:
						this.groupGentle[index].active = !this.groupGentle[index].active;
						this.groupGentleArr = this.groupGentle.filter(v => {
							return v.active
						});
						let count1 = 0;
						this.groupGentleArr.map(item => {
							if (item.active) {
								count1 += item.pour
							}
						})
						this.acount = count1;
						break;
					case 6:
						if (wei == 1) {
							this.shi[index].active = !this.shi[index].active;
						};
						if (wei == 2) {
							this.ge[index].active = !this.ge[index].active;
						};
						this.shiarr = this.shi.filter(v => {
							return v.active
						})
						this.gearr = this.ge.filter(v => {
							return v.active
						})
						if (this.shiarr.length == 1 && this.gearr.length == 1) {
							if (this.shiarr[0].num == this.gearr[0].num) {
								this.acount = 0;
								this.total = "每位至少选择1个不同的号码"
								return;
							}
						}
						let count3 = 0;
						this.shiarr.map(shi => {
							this.gearr.map(ge => {
								if (shi.num != ge.num) {
									count3++;
								}
							})
						})
						this.acount = count3;
						break;
				}
				this.total = this.acount * 2;
			},
			clear() {
				this.shi.map(v => {
					v.active = false;
				});
				this.bai.map(v => {
					v.active = false;
				});
				this.ge.map(v => {
					v.active = false;
				});
				this.san.map(v => {
					v.active = false;
					v.isGallbladder = false;
				});
				this.liu.map(v => {
					v.active = false;
					v.isGallbladder = false;
				});
				this.directlyElectedGentle.map(v => {
					v.active = false;
				});
				this.groupGentle.map(v => {
					v.active = false;
				});
				this.redLength = 0;
				this.blueLength = 0;
				this.total = 0
				this.acount = 0
				this.shiarr = []
				this.baiarr = []
				this.gearr = []
				this.sanarr = []
				this.liuarr = []
				this.directlyElectedGentleArr = []
				this.groupGentleArr = []
			},
			//tab切换事件
			changeSelectBall(item, type) {
				this.zindex = item.index
				this.clear();
			},
			//机选
			randomSelect() {
				this.clear();
				if (this.zindex == 0 && this.current == 0) {
					let numberArr = this.globalUtil.randomFromZero(10, 3);
					this.bai[numberArr[0]].active = true
					this.shi[numberArr[1]].active = true
					this.ge[numberArr[2]].active = true
					this.shiarr = this.shi.filter(v => {
						return v.active
					})
					this.baiarr = this.bai.filter(v => {
						return v.active
					})
					this.gearr = this.ge.filter(v => {
						return v.active
					})
					this.acount = this.globalUtil.math(this.baiarr.length, 1) * this.globalUtil.math(this.shiarr.length,
						1) * this.globalUtil.math(
						this.gearr.length, 1)
				} else if (this.zindex == 1 && this.current == 0) {
					let numberArr = this.globalUtil.randomFromZero(28, 1);
					this.directlyElectedGentle[numberArr[0]].active = true
					this.directlyElectedGentleArr = this.directlyElectedGentle.filter(v => {
						return v.active
					})
					this.acount = this.directlyElectedGentle[numberArr[0]].pour;
				} else if (this.zindex == 0 && this.current == 1) {
					let numberArr = this.globalUtil.randomFromZero(10, 2);
					for (var i = 0; i < numberArr.length; i++) {
						this.san[numberArr[i]].active = true
					}
					this.sanarr = this.san.filter(v => {
						return v.active
					});
					this.acount = this.globalUtil.math(this.sanarr.length, 2) * 2;
				} else if (this.zindex == 1 && this.current == 1) {
					let numberArr = this.globalUtil.randomFromZero(10, 3);
					for (var i = 0; i < numberArr.length; i++) {
						this.liu[numberArr[i]].active = true;
					}
					this.liuarr = this.liu.filter(v => {
						return v.active
					});
					this.acount = this.globalUtil.math(this.liuarr.length, 3);
				} else if (this.zindex == 2 && this.current == 1) {
					let numberArr = this.globalUtil.randomFromZero(26, 1);
					this.groupGentle[numberArr[0]].active = true
					this.groupGentleArr = this.groupGentle.filter(v => {
						return v.active
					})
					this.acount = this.groupGentle[numberArr[0]].pour;
				} else if (this.zindex == 3 && this.current == 1) {
					let numberArr = this.globalUtil.randomFromZero(10, 2);
					this.shi[numberArr[0]].active = true
					this.ge[numberArr[1]].active = true
					this.shiarr = this.shi.filter(v => {
						return v.active
					})
					this.gearr = this.ge.filter(v => {
						return v.active
					})
					this.acount = this.globalUtil.math(this.shiarr.length,
						1) * this.globalUtil.math(
						this.gearr.length, 1)
				}
				this.total = this.acount * 2;
			},
			sure() {
				if (this.total == 0) {
					this.randomSelect();
					return;
				}
				if (this.total == '每位至少选择1个不同的号码') {
					uni.showToast({
						title: '每位至少选择1个不同的号码',
						icon: 'none'
					});
					return;
				}
				let data;
				//随机数id用户传到购物车进行去重处理
				let uid = Math.ceil(Math.random() * 9999999999999999)
				if (this.zindex == 0 && this.current == 0) {
					data = {
						uid: uid,
						mode: 0,
						notes: this.acount,
						total: this.total,
						individual: this.gearr.map(v => {
							return v.num
						}),
						ten: this.shiarr.map(v => {
							return v.num
						}),
						hundred: this.baiarr.map(v => {
							return v.num
						})
					}
				} else if (this.zindex == 1 && this.current == 0) {
					data = {
						uid: uid,
						mode: 3,
						notes: this.acount,
						total: this.total,
						individual: this.directlyElectedGentleArr.map(v => {
							return v.num
						}),
					}
				} else if (this.zindex == 0 && this.current == 1) {
					data = {
						uid: uid,
						mode: 1,
						notes: this.acount,
						total: this.total,
						individual: this.sanarr
					}
				} else if (this.zindex == 1 && this.current == 1) {
					data = {
						uid: uid,
						mode: 2,
						notes: this.acount,
						total: this.total,
						individual: this.liuarr
					}
				} else if (this.zindex == 2 && this.current == 1) {
					data = {
						uid: uid,
						mode: 4,
						notes: this.acount,
						total: this.total,
						individual: this.groupGentleArr.map(v => {
							return v.num
						})
					}
				} else if (this.zindex == 3 && this.current == 1) {
					data = {
						uid: uid,
						mode: 5,
						notes: this.acount,
						total: this.total,
						individual: this.gearr.map(v => {
							return v.num
						}),
						ten: this.shiarr.map(v => {
							return v.num
						}),
					}
				}
				uni.navigateTo({
					url: "/pages/pailie/buyShoppingCar?obj=" + encodeURIComponent(JSON.stringify(data)),
					animationType: 'pop-in',
					animationDuration: 200
				})
			},
		},
	}
</script>
<style scoped>
	/deep/.cmd-nav-bar-right-text {
		font-size: 16px !important;
	}

	/deep/.u-checkbox-group--row {
		justify-content: center;
		align-items: center;
		margin-top: 5px;
		margin-left: 6px;
	}

	.tips {
		padding: 20rpx;
		color: #999;
		font-size: 28rpx;
	}

	.tips span {
		color: #FF3F43;
	}

	.fc {
		margin-bottom: 30rpx;
	}

	.fc ul {
		margin-top: 12rpx;
		padding-left: 36rpx;
	}

	.fc ul p {
		height: 50rpx;
		line-height: 50rpx;
		color: #fff;
		background: #FF3F43;
		width: 100rpx;
		font-size: 30rpx;
		padding-left: 20rpx;
		margin-left: -36rpx;
		border-top-right-radius: 30rpx;
		border-bottom-right-radius: 30rpx;
	}

	.fc ul li {
		display: inline-block;
		width: 74rpx;
		color: #FF3F43;
		background: #fff;
		height: 74rpx;
		text-align: center;
		line-height: 74rpx;
		font-size: 30rpx;
		border: 1px solid #e2e2e2;
		border-radius: 50%;
		margin: 18rpx
	}

	.fc ul li.active {
		background: #FF3F43;
		color: #fff;
	}

	.fc_tab {
		padding: 0 20rpx;
		background: #fff;
		height: 70rpx;
		padding-top: 30px;
	}

	.fc_tab span {
		display: inline-block;
		width: 33%;
		text-align: center;
		line-height: 10rpx;
		height: 45rpx;
		;
		font-size: 34rpx;
		float: left;
	}

	.fc_tab span.active {
		border-bottom: 1px solid #FF3F43;
		color: #FF3F43;
	}

	.fc_index {
		height: 54rpx;
		line-height: 30rpx;
		color: #999;
		font-size: 28rpx;
		background: #fff;
		text-align: center;
		padding-top: 30px;
	}
</style>

前端处理下单代码如下：
<template>
	<view class="box">

		<nav-bar :title="'排列3'" :back="true"></nav-bar>
		<div class="shoppingCar_wrap">
			<div class="shoppingCar_content">
				<div class="shoppingCar_add">
					<div class="add_once" @tap="random">+机选1注</div>
					<div class="add_back" @tap="back">+继续选号</div>
					<div class="add_back" @tap="clean">+清空列表</div>
				</div>
				<div class="shoppingCar_added">
					<div class="added_selected" v-for="arr in placeData">
						<div class="selected_left">
							<div class="selected_text">
								<div class="selected_num">
									<div class="content" v-for="a in arr.hundred">
										<p>{{a}}</p>
									</div>
									<span class="vertical" v-if="arr.hundred!=null">|
									</span>
									<div class="content" v-for="b in arr.ten">
										<p>{{b}}</p>
									</div>
									<span class="vertical" v-if="arr.ten!=null">|
									</span>
									<div class="content" v-if="type==1 || type==2" v-for="c in arr.individual">
										<p v-if="c.isGallbladder" style="font-size: 14px;">
											{{'胆'+c.num}}
										</p>
										<p v-else>{{c.num}}</p>
									</div>
									<div v-if="type!=1 &&type!=2" class="content" v-for="c in arr.individual">
										<p>{{c}}</p>
									</div>
								</div>
								<div class="selected_count">
									{{arr.mode|formatMode}} {{arr.notes}}注 {{arr.total}}元
								</div>
							</div>
						</div>
						<u-icon @tap="del(arr.uid)" name="trash" size="26" color="#909399"></u-icon>
					</div>
					<div class="added_rule">
						<div class="rule_left">
							<span>购买即同意《委托投注协议》</span>
						</div>
					</div>
				</div>
			</div>
			<div class="shoppingCar_footer">
				<view style="display: flex; justify-content: center;align-items: center;">
					投<u-number-box iconStyle="color: #FF3F43" integer inputWidth="70" @change="numberChange">
					</u-number-box>倍
				</view>
				<div class="footer_bottom">
					<div class="bottom_left">
						共 <b>{{acount}}</b>注 <b>{{total}}</b>元
					</div>
					<div class="bottom_right">
						<span @tap="() => confirmIsShow = true">下一步</span>
					</div>
				</div>
			</div>
		</div>
		<u-modal title="投注确认" :show="confirmIsShow" :zoom="false" confirmText="投注" showCancelButton
			confirmColor="#FF3F43" @confirm="betting" @cancel="() => confirmIsShow = false">
			<view class="tip">
				<p>[排列3]</p>
				<p>第{{issueNo}}期</p>
				<p>共{{acount}}注，您需要支付{{total}}元</p>
			</view>
		</u-modal>

	</view>
</template>

<script>
	import {
		place,
		getIssueNo
	} from '@/api/pailie.js'
	export default {
		data() {
			return {
				type: "",
				confirmIsShow: false,
				placeData: [],
				total: 0,
				acount: 0,
				times: 1,
				issueNo: ""
			}
		},
		filters: {
			formatMode(data) {
				if (data == 0) {
					return "直选"
				} else if (data == 1) {
					return "组三"
				} else if (data == 2) {
					return "组六"
				} else if (data == 3) {
					return "直选和值"
				} else if (data == 4) {
					return "组选和值"
				} else if (data == 5) {
					return "组三单式"
				}
			}
		},
		onLoad(option) {
			if (option.obj != undefined) {
				let obj = JSON.parse(decodeURIComponent(option.obj));
				this.type = obj.mode;
				this.calculation(obj);
			}
			//当前期号
			getIssueNo("3").then(res => {
				this.issueNo = res.stageNumber
			})
		},
		methods: {
			//投注
			betting() {
				uni.showLoading();
				let data = uni.getStorageSync('pailie');
				if (data.length <= 0) {
					uni.showToast({
						title: '至少选择一注',
						icon: 'none'
					});
					return;
				}
				if (this.total < 10) {
					uni.showToast({
						title: '下单金额最低10元起投',
						icon: 'none'
					});
					return;
				}
				//往数组中添加倍数新字段
				data.forEach(item => {
					this.$set(item, 'times', this.times)
					delete item['total']
					delete item['uid']
				})
				place(data, "3").then(res => {
					if (res.success) {
						uni.showToast({
							title: '下单成功',
							icon: 'none'
						});
						//标识为已经下单了
						uni.setStorageSync('isPay', true);
						this.clean();
						this.confirmIsShow = false;
						setTimeout(function() {
							uni.hideLoading();
						}, 500);
						uni.navigateTo({
							url: "/pages/order/lotteryOrderDetails?id=" + res.id,
							animationType: 'pop-in',
							animationDuration: 200
						})
					}
				})
			},
			//计算
			calculation(obj) {
				let data = uni.getStorageSync('pailie');
				let isRepeat = false
				if (data.length > 0) {
					data.map(item => {
						//如果有重复进行标记
						if (item.uid == obj.uid) {
							isRepeat = true;
							return;
						}
					})
					//根据标记去重处理
					if (!isRepeat) {
						//如果不是重复的继续叠加
						data.unshift(obj)
						uni.setStorageSync("pailie", data)
					}
					//赋值
					this.placeData = data
					//计算总价和总注数
					data.map(item => {
						this.total += item.total
						this.acount += item.notes
					})
				} else {
					//第一次为空的时候写入到本地缓存
					this.placeData.push(obj)
					uni.setStorageSync("pailie", this.placeData)
					this.total = obj.total;
					this.acount = obj.notes;
				}
			},
			//机选
			random() {
				this.total = 0;
				this.acount = 0;
				let uid = Math.ceil(Math.random() * 9999999999999999)
				if (this.type == 0 || this.type == 3) {
					let arr = this.globalUtil.randomFromZero(10, 3);
					let obj = {
						uid: uid,
						mode: 0,
						notes: 1,
						total: 2,
						individual: [arr[0]],
						ten: [arr[1]],
						hundred: [arr[2]]
					}
					this.calculation(obj);
				} else if (this.type == 1) {
					let arr = this.globalUtil.randomFromZero(10, 2);
					let data = [];
					//组装排3数据
					for (var i = 0; i < arr.length; i++) {
						data.push({
							num: arr[i],
							active: false,
							isGallbladder: false
						})
					}
					let obj = {
						uid: uid,
						mode: 1,
						notes: 2,
						total: 4,
						individual: data,
					}
					this.calculation(obj);
				} else if (this.type == 2) {
					let arr = this.globalUtil.randomFromZero(10, 3);
					let data = [];
					//组装排3数据
					for (var i = 0; i < arr.length; i++) {
						data.push({
							num: arr[i],
							active: false,
							isGallbladder: false
						})
					}
					let obj = {
						uid: uid,
						mode: 2,
						notes: 1,
						total: 2,
						individual: data,
					}
					this.calculation(obj);
				} else if (this.type == 4 || this.type == 5) {
					let arr = this.globalUtil.randomFromZero(10, 3);
					let obj = {
						uid: uid,
						mode: 2,
						notes: 1,
						total: 2,
						individual: arr,
					}
					this.calculation(obj);
				}
			},
			//删除
			del(uid) {
				let data = uni.getStorageSync('pailie');
				//重新计算总价和总注数
				data.map(item => {
					if (item.uid == uid) {
						this.total -= item.total
						this.acount -= item.notes
					}
				})
				//删除数据
				data = data.filter((item) => {
					return item.uid != uid;
				});
				//重新赋值
				this.placeData = data
				//写入缓存
				uni.setStorageSync("pailie", data)
			},
			numberChange(item) {
				this.total = this.acount * item.value * 2
				this.times = item.value;
			},
			back() {
				uni.navigateBack();
			},
			//清空
			clean() {
				uni.removeStorageSync("pailie")
				this.placeData = []
				this.total = 0;
				this.acount = 0;
			}
		},
	}
</script>

<style scoped lang="scss">
	.vertical {
		color: #848484;
		padding: 0 10rpx;
	}

	.content {
		width: 25px;
		height: 25px;
		background-color: #FF3F43;
		border-radius: 50%;
		display: inline-block;
		margin-right: 2px;

		p {
			width: 25px;
			height: 25px;
			color: #fff;
			text-align: center;
			line-height: 25px;
			font-size: 16px;
		}
	}

	.tip {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;

		p {
			margin-top: 8rpx;
			color: #606266;
			font-size: 16px;
		}
	}

	.shoppingCar_wrap {
		.shoppingCar_content {
			.shoppingCar_add {
				margin-bottom: 2.26667vmin;
				font-size: 3.73333vmin;
				padding: 0 3.33333vmin;
				display: flex;
				align-items: center;
				justify-content: space-between;

				div {
					width: 48%;
					background-color: white;
					height: 11.46667vmin;
					display: flex;
					justify-content: center;
					align-items: center;
					color: #666;
				}
			}

			.shoppingCar_added {
				box-sizing: border-box;
				margin: 0 26rpx;

				.added_rule {
					box-sizing: border-box;
					font-size: 3.46667vmin;
					height: 12.53333vmin;
					width: 100%;
					background-color: white;
					color: #999;
					display: flex;
					align-items: center;
					justify-content: space-between;
					padding: 0 4.4vmin;
				}

				.added_selected {
					background-color: white;
					padding: 2.66667vmin;
					box-sizing: border-box;
					border-bottom: 1px solid #e6e6e6;
					display: flex;
					align-items: center;
					justify-content: space-between;

					.selected_left {
						display: flex;
						align-items: center;
						justify-content: center;

						.selected_text {

							.selected_num {
								color: #FF5562;
								font-size: 5.33333vmin;
								margin-bottom: 1.8vmin;
							}

							.selected_count {
								font-size: 3.46667vmin;
								color: #999;
							}
						}
					}
				}
			}
		}

		.shoppingCar_footer {
			width: 100%;
			position: fixed;
			bottom: 0;
			left: 0;
			color: #8f9090;
			background-color: white;

			.footer_bottom {
				box-sizing: border-box;
				width: 100%;
				display: flex;
				align-items: center;
				justify-content: space-between;
				height: 13.33333vmin;
				padding-left: 2.66667vmin;

				.bottom_left {
					color: #333333;
					font-size: 4vmin;

					b {
						color: #FF5562;
					}
				}

				.bottom_right {
					/*border: none;*/
					text-align: center;
					background: #FF3F43;
					color: #FFFFFF;
					font-size: 4.8vmin;
					width: 28.53333vmin;
					border-radius: 4px;
					height: 100%;
					display: flex;
					align-items: center;
					justify-content: center;
				}
			}
		}
	}
</style>

API接口代码如下：
import request from '@/util/ajax'


/**
 * 排列下单
 * @param {Object} data
 */
export function place(data,type) {
	return request({
		url: '/app/permutation/place/'+type,
		method: 'post',
		data
	})
}

/**
 * 历史排列开奖记录
 */
export function record(type) {
	return request({
		url: '/app/permutation/record/'+type,
		method: 'get',
	})
}

/**
 * 获取排列期号接口
 */
export function getIssueNo(type) {
	return request({
		url: '/app/permutation/issue/'+type,
		method: 'get',
	})
}
