## 代码逻辑

* 声明变量：

```go
//增加指标cpu占用率
cpu_occupancy = prometheus.NewGauge(prometheus.GaugeOpts{
			Name:	   "CPU_Occupancy_Rate",
			Help:	   "The Occupancy Rate of CPU.",
	})
```

* 注册变量

  ```go
  //在prometheus节点上注册改变量
  prometheus.MustRegister(cpu_occupancy)
  ```

* 逻辑实现

  ```
  // cpu使用率
  	percent,_:=cpu.Percent(time.Second,false)
  	cpu_occupancy.Set(percent[0])
  }
  ```

调用了`gopsutil`库来监控CPU的占用率，每秒刷新一次。

#### 结果截图

![](result.png)
