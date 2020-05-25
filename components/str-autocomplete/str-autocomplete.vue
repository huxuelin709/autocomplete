<template>
    <view>
        <input class="uni-input" placeholder="请输入内容" :value="value" @input="onInput" @blur="hideList"/>
        <view class="str-auto-complete-container" v-if="isShow">
            <view v-for="(item, index) in showList" :key="index" class="str-auto-complete-item" @tap="selectThisItem(item)" v-html="item.showString"></view>
        </view>
    </view>
</template>

<script>
export default {
    props: {
        stringList: {
            type: Array
        },
		importvalue: {
			type: String
		},
		lowerAndUp: {
			type: String,
			default: "true"
		},
        highlightColor: {
            type: String,
            default: 'lightcoral'
        }
    },
    data() {
        return {
            showList: [],
            value: '',
            needShow: false
        };
    },
	watch: {
		importvalue(newValue, oldValue) {
			this.value = newValue
		},
		stringList: {
	　　　　handler(newValue, oldValue) {
				this.filterList(this.value);
	　　　　},
	　　　　deep: true
	　　}
	},
    model: {
        prop: 'value',
        event: 'change'
    },
    computed: {
        isShow() {
            return this.needShow && this.showList.length > 0;
        }
    },
    created() {
        this.stringList.sort();
        this.showList = this.stringList;
		this.value = this.importvalue;
    },
    methods: {
        onInput(event) {
            this.filterList(event.target.value);
			this.$set(this, 'value', event.target.value);
            this.$emit('change', event.target.value);
            if (event.target.value.length > 0) {
                this.needShow = true;
            } else {
                this.needShow = false;
            }
        },
		hideList() {
			setTimeout(() => {
				this.needShow = false;
			}, 300);
			
		},
        filterList(stringExp) {
            let tempArray = [];
            for (let i = 0; i < this.stringList.length; i++) {
                let temp = this.stringList[i];
                let showObject = this.filterString(stringExp, temp);
                if (showObject) {
                    if (showObject.number === stringExp.length) {
                        tempArray.push(showObject);
                    }
                }
            }
            if (tempArray.length === 0 && stringExp.length !== 0) {
                uni.showToast({
                    title: '没有匹配的字符串',
                    mask: false,
                    icon: 'none',
                    duration: 1500
                });
                return false;
            }
            this.showList = tempArray;
        },
        filterString(stringExp, b) {
            const tempByteArray = b.split('');
            let itemShow = [];
            const sArray = stringExp.split('');
            const fontStart = '<span style=color:' + this.highlightColor + '>';
            const fontEnd = '</span>';
            let sameCharNumber = 0;
            for (let j = 0; j < tempByteArray.length; j++) {
				let tempChar = tempByteArray[j];
				let sChar = sArray[sameCharNumber];
				if (this.lowerAndUp !== 'no') {
					tempChar = tempChar.toLowerCase();
					if (sChar) {
						sChar = sChar.toLowerCase();
					}
				}
				
				
                if (tempChar === sChar) {
                    let sameNumberNow = sameCharNumber;
                    itemShow.push(fontStart);
                    for (let k = 0; k < sArray.length - sameNumberNow; k++) {
						let tempCharStr = tempByteArray[j + k] || '';
						let sCharStr = sArray[k + sameNumberNow];
						if (this.lowerAndUp !== 'no') {
							tempCharStr = tempCharStr.toLowerCase();
							if (sCharStr) {
								sCharStr = sCharStr.toLowerCase();
							}
						}
						
                        if (tempCharStr === sCharStr) {
                            itemShow.push(tempByteArray[j + k]);
                            sameCharNumber++;
                        } else if (tempCharStr !== sCharStr) {
                            itemShow.push(fontEnd);
                            itemShow.push(tempByteArray[j + k]);
                            j += k;
                            break;
                        }
                        if (k + sameNumberNow === sArray.length - 1) {
                            j += k;
                            itemShow.push(fontEnd);
                        }
                    }
                } else {
                    itemShow.push(tempByteArray[j]);
                }
            }
            if (sameCharNumber > 0) {
                return {
                    orginalString: b,
                    number: sameCharNumber,
                    showString: itemShow.join('')
                };
            }
        },
        selectThisItem(item) {
			this.$set(this, 'value', item.orginalString);
            this.needShow = false;
            this.$emit('change', item.orginalString);
			this.$emit('select', item.orginalString);
        }
    }
};
</script>

<style lang="scss">
.str-auto-complete-container {
    width: 60%;
    height: auto;
    border: 1px solid #f3f3f4;
    position: absolute;
    z-index: 999;
    background: #fff;
    .str-auto-complete-item {
        padding: 10upx;
    }
}
</style>
