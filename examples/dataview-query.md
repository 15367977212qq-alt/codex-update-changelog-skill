# Dataview Query Example

```dataview
TABLE date AS 日期, file.link AS 日志, source AS 来源
FROM "bi_project/CHANGELOG"
WHERE type = "changelog" AND project = "bi_project"
SORT date DESC
LIMIT 10


注意：如果 Markdown 文件里要展示 Dataview 代码块，外层需要用四个反引号包起来，避免代码块提前结束。