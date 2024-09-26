# Clash-Verge-订阅/配置 自动切换

// 脚本实现不同 订阅/配置 添加不同规则  
// 使用：复制全部内容到verge的全局扩展脚本中，然后根据需求修改  
// 此脚本模板适用于verge-rev的1.7.3以上版本，适用于多场景、多设备使用  
// 示例脚本仅包含：针对使用订阅，进行规则字段内容的 覆盖 以及对其进行prepend/append  
// 针对筛选的订阅进行分组、规则等字段内容的覆盖以及对其rules、proxies、rule-providers进行prepend/append  
// 请参考 https://github.com/Kiritocyz/Clash/  

// Define main function (script entry)  

// 自定义规则，针对需求，可以是多个 const 变量  
const rules = [  
  'PROCESS-NAME,ChatGPT,🔰 节点选择', // ChatGPT  
  'DOMAIN-SUFFIX,chatgpt.com,🔰 节点选择', //网页ChatGPT  
  'DOMAIN-SUFFIX,openai.com,🔰 节点选择', //openai  
  'DOMAIN-SUFFIX,ai.google.dev,🔰 节点选择 ', //google ai  
  'DOMAIN-SUFFIX,local, DIRECT', // 本地  
  'MATCH,DIRECT', // 剩下的  
];  
  
// 自定义规则2，  
const rules2 = [  
  // .. 其他规则  
];  

// 自定义规则3  
const rules3 = [  
  // .. 其他规则  
];  
  
function main(config, profileName) {  
  console.log("Profile Name: " + profileName);  
  
  //第一个匹配规则  
  const pattern_1 = /^hk-.*/; //这里需要注意，表达式写在里面 /正则表达式/  
  const pattern_2 = /.pattern2.*/; //这里需要注意，表达式写在里面 /正则表达式/  
  if (profileName.match(pattern_1)) {  
    // 以下按照需求排列组合使用  
    // 前部附加规则  
    config.rules.unshift(rules1);  
    // 后部附加规则  
    config.rules.push(rules2);  
    // 覆盖配置  
    config['rules'] = rules3  
  }  
  if (profileName.match(pattern_2)) {  
    // 合并规则  
    config['rules'] = rules  
  }  

  return config;  
}  
