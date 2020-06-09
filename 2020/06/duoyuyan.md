# 1. 项目基础
- Ant Desig(前端框架)
- React
- Redux
- axios
# 2. 多语言
## 1. 组件多语言
- Ant Design 自带的国际化组件, [参考官网](https://ant.design/components/config-provider-cn/)
- 全局化配置组件的国际化， 包裹根组件
- local 是配置的语言包

    ```javascript

    import enUS from 'antd/es/locale/en_US';
    import zhCN from 'antd/es/locale/zh_CN';
    
    <ConfigProvider locale={enUS}>
        <App />
    </ConfigProvider>
    ```

## 2. 业务的多语言
- 借助于 react-intl 语言包
    ```javascript
        npm i react-intl --save
    ```
- 使用 react-intl, 全局引入配置
    ```javascript
        //main.js
        // 引入local config
        import zh from 'locals/zh'
        import en from 'locals/en'
        <IntlProvider locale={zh} messages={zh} >
            <ConfigProvider locale={enUS}>
            <App />
            </ConfigProvider>
        </IntlProvider>

        // locales
        //en.js
        export default {
            helllo: 'Hello'
        }
        //zh.js
        export default {
            helllo: '你好'
        }
    ```
- 业务中的文本多语言 
    ```javascript
       // 文本
        import { FormattedMessage } from 'react-intl';
        <button><FormattedMessage id='helllo' /></button>
        // en
        Hello
        //zh
        你好
    ```
- Class中组件的属性的多语言(根据Ant Design组件为例)
    ```javascript
       // 组件属性, 先注入
        import { injectIntl } from 'react-intl';
        import { connect} fron 'react-redux'
        // 注入到calss 
        class Demo {
          
        }

        export default injectIntl (Demo)
        // or 利用reudx
        class Demo {

        }

        export default connect(mapStateToProps,mapActionCreators)(injectIntl(Demo))
       
    ```
    ```javascript

       // 组件属性, 在props 中进行引用
       const { intl } = this.props;

       const demo = intl.formatMessage({ id: 'hello' })

       <input lable={demo} placeholder={demo} />

       // en
        <input lable='Hello' placeholder='Hello' />

        //zh
        <input lable='你好' placeholder='你好' />
       
    ```
- Hook 中使用
    ```javascript

       // 组件属性, 注入的方法不一样
       import { useIntl } from 'react-intl';
       const intl = useIntl();

       const demo = intl.formatMessage({ id: 'hello' })

       <input lable={demo} placeholder={demo} />

       // en
        <input lable='Hello' placeholder='Hello' />

        //zh
        <input lable='你好' placeholder='你好' />
       
    ```
