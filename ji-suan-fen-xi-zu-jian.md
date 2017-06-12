# 计算分析组件

---

计算分析组件是计算分析平台的最小执行单元。计算分析组件的作用是能够执行分析平台下达的计算分析任务。每个计算组件完成特殊的功能，每个计算组件根据业务的需要可大可小。例如，读取文件中的关键参数可以认为是个计算分析组件，对输入的参数进行数据处理也可以认为是个计算组件；但是每个计算组件必须满足平台给定的规范。

## 计算分析组件的后台规范

* 普通组件的规范

```java
package com.orient.analysisflow.component;

import java.util.List;
import java.util.Map;

/**
 *
 *  分析组件的的规范
 * @author mengbin
 * @create 2017-03-14 下午3:36
 */
public interface AnalysisComponentRule {


    /**
     * 获得组件名称
     * @return
     */
    String getName();

    /**
     * 获得组件动态的加载类名
     * @return
     */
    String getComponentClassName();


    /**
     * 获得组件的描述
     * @return
     */
    String getDesc();


    /**
     * 获取组件的输出结构
     * @return
     */
    List<AnalysisComponentIO> getOutPut();


    /**
     * 获取该组件的输入结构
     * @return
     */
    List<AnalysisComponentIO> getInPut();


    /**
     * 是否要打断
     * @return
     */
    boolean isInterrupt();

    /**
     * 结果是否要显示
     * @return
     */
    boolean isResultShow();


    /**
     * 结果数据
     * @return
     */
    Map<String,Object> getShowData();


    /**
     * 获取要设置的参数
     * @return
     */
    Map<String,AnalysisInterruptParam> getInterruptParams();

    /**
     * 设置参数
     * @param params
     * @return
     */
    boolean setInterruptParams(Map<String,AnalysisInterruptParam> params);

    /**
     * 设置组件运行的通用参数
     * @param json
     * @return
     */
    boolean setConfigJson(String json);

    /**
     * 执行组件
     * @param inputData
     * @return
     */
    boolean exec(List<AnalysisComponentIO> inputData);


}

```



