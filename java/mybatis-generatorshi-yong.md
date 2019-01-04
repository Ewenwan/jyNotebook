* 导入项目
* 配置文件

  * generatorConfig.xml

  ```
     去掉注释
       <commentGenerator>
          <property name="suppressDate" value="true"/>
          <property name="suppressAllComments" value="true" />
        </commentGenerator>
  ```

  * mybatis-generator-config\_1\_0.dtd

各类包及其类

![](/assets/java-1.12-1.png)

* com.crm.entity

  * PageResult.java

  \`\`\`  
  package com.crm.entity;

  import java.util.List;

  public class PageResult {  
      private Integer total;  
      private List rows;

  ```
  public PageResult() {
      super();
  }

  public PageResult(Integer total, List rows) {
      super();
      this.total = total;
      this.rows = rows;
  }

  public Integer getTotal() {
      return total;
  }

  public void setTotal(Integer total) {
      this.total = total;
  }

  public List getRows() {
      return rows;
  }

  public void setRows(List rows) {
      this.rows = rows;
  }
  ```

}

\`\`\`

* 


