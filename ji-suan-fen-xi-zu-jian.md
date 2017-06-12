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

* 判断组件规范

```java
package com.orient.analysisflow.decision;

import com.orient.analysisflow.component.AnalysisComponentRule;
import com.orient.analysisflow.component.AnalysisComponentIO;

import java.util.List;

/**
 * ${DESCRIPTION}
 *
 * @author mengbin
 * @create 2017-03-21 下午3:20
 */
public interface AnalysisDecisionRule extends AnalysisComponentRule{


    /**
     * 获取组件控制流中不同的流向
     * @return
     */
    public List<String> getSelfOutComes();

    /**
     *
     * @param inputData 输入的数据
     * @param outComeIndex 输出的outcome的索引,从0开始
     * @return
     */
    boolean exec(List<AnalysisComponentIO> inputData, StringBuffer outComeIndex);



}
```

* 组件数据流转规范

```java
package com.orient.analysisflow.component;

import java.lang.reflect.Type;

/**
 * 组件的输入输出规范
 *
 * @author mengbin
 * @create 2017-03-14 下午3:40
 */
public interface AnalysisComponentIO {

    /**
     * 获取参数名称
     * @return
     */
    public String getName();


    /**
     * 返回是输入还是输出 0: 输入 , 1:输出
     * @return
     */
    public int getType();


    /**
     * 获取数据存储的类型 0: file 1 : 基础数据类型 具体类型根据datatype
     * @return
     */
    public int getStorageType();

    /**
     * 获取数据的类型
     * @return
     */
    public Type getDataType();


    /**
     * 0: 自定义的数据文件 1:表示规范的数据文件
     * @return
     */
    public int getFileType();


    /**
     *标准数据文件中矩阵的维度
     * @return
     */
    public int getDimensionCount();


    /**
     * 获取标准数据文件中矩阵数据的类型
     * @return
     */
    public Type getDimensionType();


    //===================================================//
    /**
     *
     * 运行时使用
     *
     */
    //===================================================//

    /**
     * 获取基础数据的值
     * @return
     */
    public Object getDataValue();

    /**
     * 获取每一维度中数据的个数 如果是 0 表示任意长度
     * @return
     */
    public int[] getDimensionDataCount();

    public void setDataValue(Object obj);

    public void setDimensionDataCount(int[] dataCount);

}
```

* 用户输入参数规范

```java
package com.orient.analysisflow.component;

/**
 * Created by mengbin on 2017/5/22.
 */
public  class AnalysisInterruptParam {
    String name;
    int    type;
    String showValue;
    String data;

    static public int TYPE_INT = 0;
    static public int TYPE_DOUBLE = 1;
    static public int TYPE_FLOAT = 2;
    static public int TYPE_FILE = 3;
    static public int TYPE_STRING = 4;
    static public int TYPE_BOOLEAN = 5;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getType() {
        return type;
    }

    public void setType(int type) {
        this.type = type;
    }

    public String getShowValue() {
        return showValue;
    }

    public void setShowValue(String showValue) {
        this.showValue = showValue;
    }

    public String getData() {
        return data;
    }

    public void setData(String data) {
        this.data = data;
    }
}
```

* ## 计算分析组件的前台规范
* 组件结果显示的规范

* 组件配置信息设置的前台规范



