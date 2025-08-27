/**
 * 需要前置的学术类直连规则
 * 格式说明：DOMAIN-SUFFIX,域名,DIRECT
 */
const prependRule = [

  // 综合学术出版
  "DOMAIN-SUFFIX,ieee.org,DIRECT",          // IEEE Xplore
  "DOMAIN-SUFFIX,elsevier.com,DIRECT",      // 爱斯维尔 (Elsevier)
  "DOMAIN-SUFFIX,sciencedirect.com,DIRECT", // ScienceDirect
  "DOMAIN-SUFFIX,sciencedirectassets.com,DIRECT", // ScienceDirectPdf
  "DOMAIN-SUFFIX,springer.com,DIRECT",      // Springer
  "DOMAIN-SUFFIX,science.org,DIRECT",        // science
  "DOMAIN-SUFFIX,nature.com,DIRECT",        // Nature
  
  // 学术数据库
  "DOMAIN-SUFFIX,clarivate.com,DIRECT",     // Web of Science
  "DOMAIN-SUFFIX,jstor.org,DIRECT",         // JSTOR
  "DOMAIN-SUFFIX,proquest.com,DIRECT",      // ProQuest
  
  // 学术搜索引擎
  "DOMAIN-SUFFIX,semanticscholar.org,DIRECT", // Semantic Scholar
  "DOMAIN-SUFFIX,researchgate.net,DIRECT",    // ResearchGate
  
  // 医学专业
  "DOMAIN-SUFFIX,pubmed.ncbi.nlm.nih.gov,DIRECT", // PubMed
  "DOMAIN-SUFFIX,lancet.com,DIRECT",          // The Lancet
  
  // 中国学术资源
  "DOMAIN-SUFFIX,cnki.net,DIRECT",           // 中国知网
  "DOMAIN-SUFFIX,wanfangdata.com.cn,DIRECT", // 万方数据
  "DOMAIN-SUFFIX,cqvip.com,DIRECT"           // 维普网
];

function main(config) {
  // 合并规则（旧规则追加到新规则后面）
  const oldRules = config.rules || [];
  config.rules = [...new Set([...prependRule, ...oldRules])]; // 使用Set去重
  
  return config;
}