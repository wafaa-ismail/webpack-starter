# Webpack

#### Babel -> Babel is the javascript compiler which will convert the next generation javascript(es6) to the es5 so that the old browsers can understand the code.

#### Webpack -> Webpack is the module bundler which will compile all the javascript files or modules into single file called as bundle.


```js 
webpack.config.js

const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const BundleAnalyzerPlugin = require('webpack-bundle-analyzer').BundleAnalyzerPlugin

module.exports = {
    mode: 'development',
    entry: {
        bundle: path.resolve(__dirname, 'src/index.js') // you can add multiple entry
    },
    output: {
        path: path.resolve(__dirname, 'dist'),
        filename: '[name][contenthash].js' // get file name from entry name so it will be `bundlebe6e08fec5731e6f7eaa.js
        clean:true, //to prevent saving multiple bundle.js files 
        assetModuleFilename:'[name][ext]'

    },
    //configure dev server 
    // add     "dev": "webpack serve" in package.json then run npm run dev
    devServer:{
        static:{
            directory:path.resolve(__dirname,'dist')
        },
        port:3000,
        hot:true,
        open:true,
        compress:true,
        historyApiFallback:true
        
    },
    // add loader for scss files 
    module:{
        rules:[
            {
                test:/\.scss$/,
                use:['style-loader','css-loader','sass-loader']
            }
        ]
    },
    //load babel
    {
                test: /\.js$/,
                exclude: /node_modules/,
                use: {
                    loader: 'babel-loader',
                    options: {
                        presets: ['@babel/preset-env']
                    }
                }
            },
    //load Assets 
    {
                test:/\.(png|svg|jpg|jpeg|gif)$/i,
                type:'asset/resource'
            }
    //automatically create html in our dist folder with same templete we provide 
    plugins:[
        new HtmlWebpackPlugin({
            title:'Webpack App',
            filename:'index.html',
            template:'src/template.html'
        }),
        BundleAnalyzerPlugin()
    ]
}
```
