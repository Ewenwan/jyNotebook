* 导入项目
* 配置文件

  * generatorConfig.xml

  ```
  去掉注释


   <context id="DB2Tables" targetRuntime="MyBatis3">
    
      <commentGenerator>
      	<property name="suppressDate" value="true"/>
      	<property name="suppressAllComments" value="true" />
    	</commentGenerator>

  ```

  * mybatis-generator-config\_1\_0.dtd



