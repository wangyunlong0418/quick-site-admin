<template>
  <div>
    <Header @save="handleSaveClick"/>
    <div :style="{height: screenHeight + 'px'}">

      <component-tabs
        :style="style.componentTabs"
        :components="components"
        @click="handleTabClick"></component-tabs>

      <phone-box
        :style="style.phoneBox"
        :designs="designs"
        :editing="editing"
        @click="handleDesignClick"></phone-box>

      <setting-box
        :style="style.settingBox"
        :editing="editing"></setting-box>

    </div>
  </div>
</template>

<script>
import Header from '../components/Header'
import ComponentTabs from '../components/ComponentTabs'
import PhoneBox from '../components/PhoneBox'
import SettingBox from '../components/SettingBox'
import TitlePreview from '../components/title/TitlePreview'
import TitleSetting from '../components/title/TitleSetting'
import TextPreview from '../components/text/TextPreview'
import TextSetting from '../components/text/TextSetting'
import WhitePreview from '../components/white/WhitePreview'
import WhiteSetting from '../components/white/WhiteSetting'
import CompanyInfoPreview from '../components/companyInfo/CompanyInfoPreview'
import CompanyInfoSetting from '../components/companyInfo/CompanyInfoSetting'
import CompanyConsultPreview from '../components/companyConsult/CompanyConsultPreview'
import CompanyConsultSetting from '../components/companyConsult/CompanyConsultSetting'
import PhonePreview from '../components/phone/PhonePreview'
import PhoneSetting from '../components/phone/PhoneSetting'
import ImagePreview from '../components/image/ImagePreview'
import ImageSetting from '../components/image/ImageSetting'
import ManageTeamPreview from '../components/manageTeam/ManageTeamPreview'
import ManageTeamSetting from '../components/manageTeam/ManageTeamSetting'
import CompanyPartnerPreview from '../components/companyPartner/CompanyPartnerPreview'
import CompanyPartnerSetting from '../components/companyPartner/CompanyPartnerSetting'
import AddressPreview from '../components/address/AddressPreview'
import AddressSetting from '../components/address/AddressSetting'
import ContactMePreview from '../components/contactMe/ContactMePreview'
import ContactMeSetting from '../components/contactMe/ContactMeSetting'

export default {
  name: 'ColEditWindow',
  components: { Header, ComponentTabs, PhoneBox, SettingBox },
  data: function () {
    return {
      // 屏幕尺寸
      screenHeight: 0,
      screenWidth: 0,
      components: {
        // 模块组件数据
        modules: [
          {
            name: '企业简介',
            icon: 'font-icon font-icon-1',
            type: 1,
            preview: CompanyInfoPreview,
            setting: {
              title: '企业简介',
              component: CompanyInfoSetting
            },
            data: {
              title: '企业简介',
              content: '请填写公司简介...'
            }
          },
          {
            name: '企业咨询',
            icon: 'font-icon font-icon-2',
            type: 2,
            preview: CompanyConsultPreview,
            setting: {
              title: '企业咨询',
              component: CompanyConsultSetting
            },
            data: {
              title: '企业咨询',
              consultList: [
                { title: '咨询标题1', headImg: '', time: '2018-01-01', content: '咨询内容1', online: true },
                { title: '咨询标题2', headImg: '', time: '2018-01-01', content: '咨询内容2', online: true },
                { title: '咨询标题3', headImg: '', time: '2018-01-01', content: '咨询内容3', online: false }
              ]
            }
          },
          {
            name: '管理团队',
            icon: 'font-icon font-icon-3',
            type: 3,
            preview: ManageTeamPreview,
            setting: {
              title: '管理团队',
              component: ManageTeamSetting
            },
            data: {
              title: '管理团队',
              manageList: [
                { avatar: '', name: '张三', job: '高级Java工程师', description: '职位简介...' },
                { avatar: '', name: '姓名2', job: '职位2', description: '简介2' }
              ]
            }
          },
          {
            name: '合作伙伴',
            icon: 'font-icon font-icon-4',
            type: 4,
            preview: CompanyPartnerPreview,
            setting: {
              title: '合作伙伴',
              component: CompanyPartnerSetting
            },
            data: {
              title: '合作伙伴',
              imageList: [ '', '', '' ]
            }
          },
          {
            name: '电话',
            icon: 'font-icon font-icon-5',
            type: 5,
            preview: PhonePreview,
            setting: {
              title: '电话设置',
              component: PhoneSetting
            },
            data: {
              title: '公司电话',
              phone: '0795-XXXXXXXXX'
            }
          },
          {
            name: '地址',
            icon: 'font-icon font-icon-6',
            type: 6,
            preview: AddressPreview,
            setting: {
              title: '公司地址',
              component: AddressSetting
            },
            data: {
              title: '公司地址',
              addressDetail: '',
              lat: 0,
              lng: 0
            }
          },
          {
            name: '联系我们',
            icon: 'font-icon font-icon-7',
            type: 7,
            preview: ContactMePreview,
            setting: {
              title: '联系我们',
              component: ContactMeSetting
            },
            data: {
              title: '联系我们'
            }
          },
          {name: '企业招聘', icon: 'font-icon font-icon-8', type: 8, preview: 1, setting: 2, data: {}}
        ],
        // 基本组件数据
        basics: [
          {
            name: '标题',
            icon: 'font-icon font-icon-11',
            type: 9,
            preview: TitlePreview,
            setting: {
              title: '标题栏设置',
              component: TitleSetting
            },
            data: {
              title: '标题栏'
            }
          },
          {
            name: '文本',
            icon: 'font-icon font-icon-12',
            type: 10,
            preview: TextPreview,
            setting: {
              title: '文本设置',
              component: TextSetting
            },
            data: {
              text: '请输入内容'
            }
          },
          {
            name: '图片',
            icon: 'font-icon font-icon-13',
            type: 11,
            preview: ImagePreview,
            setting: {
              title: '图片设置',
              component: ImageSetting
            },
            data: {
              imageType: 1,
              images: []
            }
          },
          {name: '轮播图', icon: 'font-icon font-icon-14', type: 12, preview: 1, setting: 2, data: {}},
          {name: '视频', icon: 'font-icon font-icon-15', type: 13, preview: 1, setting: 2, data: {}},
          {name: '图文', icon: 'font-icon font-icon-16', type: 14, preview: 1, setting: 2, data: {}},
          {
            name: '占位符',
            icon: 'font-icon font-icon-17',
            type: 15,
            preview: WhitePreview,
            setting: {
              title: '占位符设置',
              component: WhiteSetting
            },
            data: {
              height: 10
            }
          }
        ]
      },
      // 用户正在编辑的网站数据
      designs: [],
      // 设置项
      editing: null
    }
  },
  computed: {
    style: function () {
      return {
        componentTabs: {
          float: 'left',
          width: '220px',
          height: '100%',
          overflow: 'hidden'
        },
        phoneBox: {
          float: 'left',
          width: this.screenWidth - 720 + 'px',
          height: '100%'
        },
        settingBox: {
          float: 'right',
          width: '500px',
          height: '100%',
          overflow: 'auto'
        }
      }
    }
  },
  methods: {
    handleTabClick: function (component) {
      let designData = {
        type: component.type,
        preview: component.preview,
        setting: component.setting,
        data: {
          type: component.type,
          // 深度复制
          ...JSON.parse(JSON.stringify(component.data))
        }
      }
      this.designs.push(designData)
      this.editing = designData
    },
    handleDesignClick: function (designData) {
      this.editing = designData
    },
    handleSaveClick: function () {
      console.log(JSON.stringify(this.designs.map(({data}) => ({...data}))))
    }
  },
  mounted: function () {
    const onResize = () => {
      this.screenHeight = document.body.clientHeight - 60
      this.screenWidth = document.body.clientWidth
      console.log(document.body.clientWidth)
    }
    onResize()
    window.addEventListener('resize', onResize, false)
  }
}
</script>

<style scoped>
</style>
