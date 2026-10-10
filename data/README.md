# Data Guide

[papers.json](papers.json) 为去重书目。字段：id/title/DOI/arXiv/URL/作者/首发与版本/evidence/limitations/read_first/appearances[]/provenance。appearances 为相对归档路径；可选字段未知时省略，证据可能为字符串或对象。标识优先去版本 arXiv ID、DOI、规范 URL。

历史核验来自上游 AI 辅助资料，不推断维护者实读状态。
