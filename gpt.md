
要获取ChatGPT的key，您可以按照以下步骤操作：

访问OpenAI的官方网站：https://openai.com/
单击“GET STARTED FOR FREE”按钮。
输入您的电子邮件地址，然后单击“Continue”按钮。
创建一个OpenAI账户并登录。
选择“API”选项卡，然后单击“New API Key”按钮。
输入一个名称，然后选择“Chat”作为API类型。
选择“Chinese”作为语言。
点击“Create API Key”按钮，即可获取您的ChatGPT中文版聊天插件的Key。
----

const axios = require('axios');
const vscode = require('vscode');

function activate(context) {
   // 获取ChatGPT中文版聊天API的Key
   const chatgptKey = vscode.workspace.getConfiguration().get('chatgpt.key');

   // 向ChatGPT中文版聊天API发送请求
   function sendMessage(message) {
      // 构造请求URL
      const url = `https://api.openai.com/v1/chatgpt/chinese/davinci?model=chat&prompt=${encodeURIComponent(message)}&temperature=0.7`;

      // 发送请求
      return axios.get(url, {
         headers: {
            'Authorization': `Bearer ${chatgptKey}`
         }
      }).then(response => response.data.choices[0].text);
   }

   // 注册命令
   const disposable = vscode.commands.registerCommand('extension.chatGpt', () => {
      // 获取用户输入
      vscode.window.showInputBox({ prompt: '请输入您要发送的消息' }).then(message => {
         // 发送消息并显示结果
         sendMessage(message).then(response => {
            vscode.window.showInformationMessage(response);
         });
      });
   });

   context.subscriptions.push(disposable);
}

exports.activate = activate;

function deactivate() {
   // do nothing
}

module.exports = {
   activate,
   deactivate
};