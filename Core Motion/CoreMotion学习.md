##Core Motion学习


#####Core Motion.framwork 一共有10个类
#####其中3个入口类：CMMotionManager / CMMotionActivityManager / CMStepCounter
	
	CMMotionManager		iOS提供的运动服务的入口（iOS4+）
			|
			|
			-------- CMAccelerometerData（CMLogItem子类） 加速度计数据
			|
			|
			-------- CMGyroData（CMLogItem子类） 陀螺仪数据
			|
			|
			-------- CMMagnetometerData（CMLogItem子类） 磁力仪数据
			|
			|
			-------- CMDeviceMotion（CMLogItem子类）-------- CMAttitude
			
		
	CMMotionActivityManager 提供访问存储在设备中的运动数据(iOS7+)
			|
			|
			-------- CMMotionActivity（CMLogItem子类）
		

	CMStepCouter			提供计步数据（iOS7+）
	

###CMMotionManager
#####管理加速度计/陀螺仪/磁力计/运动方向更新

@property(assign, nonatomic) NSTimeInterval accelerometerUpdateInterval 

@property(assign, nonatomic) NSTimeInterval gyroUpdateInterval

@property(assign, nonatomic) NSTimeInterval magnetometerUpdateInterval

@property(assign, nonatomic) NSTimeInterval deviceMotionUpdateInterval

	1、这个属性决定startAccelerometerUpdatesToQueue:withHandler: 
	或 startGyroUpdatesToQueue:withHandler 
	或 startMagnetometerUpdateToQueue:withHandler:
	或 startDeviceMotionUpdatesToQueue:withHandler:的频率
	
	2、最大值被硬件的最大频率制约，这个值不能超过最大频率
	
	3、如果应用对加速度计（陀螺仪、磁力计）数据的周期很敏感，本应该检查发送过来的CMAccelerometerData(CMGyroData / CMMagnetometerData / CMDeviceMotion)实例中的时间戳来确定正确的更新周期
	
-(void)startAccelerometerUpdatesToQueue:(NSOperationQueue *)queue withHandler:(CMAccelerometerHandler)handler

-(void)startGyroUpdatesToQueue:(NSOperationQueue *)queue withHandler:(CMMagnetometerHandler)handler

-(void)startMagnetometerUpdatesToQueue:(NSOperationQueue *)queue withHandler:(CMMagnetometerHandler)handler
  
-(void)startDeviceMotionUpdatesToQueue:(NSOperationQueue *)queue withHandler:(CMDeviceMotionHandler)handler

-(void)startDeviceMotionUpdatesUsingReferenceFrame:(CMAttitudeReferenceFrame)referenceFrame toQueue:(NSOperationQueue *)queue withHandler:(CMDeviceMotionHandler)handler

	1、不推荐用主线程，因为这个方法可能会以很高的频率更新。
	2、如果希望应用不再处理加速度更新，则需要调用stopAccelerometerUpdates方法
	3、deviceMotion的开始方法使用attitudeReferenceFrame返回的坐标系
	4、deviceMotion UsingReferenceFrame可以指定坐标系，其他的和startDeviceMotionUpdatesToQueue:withHandler：一样	   	

-(void)startAccelerometerUpdates

-(void)startGyroUpdates

-(void)startMagnetometerUpdates

-(void)startDeviceMotionUpdates

-(void)startDeviceMotionUpdatesUsingReferenceFrame:(CMAttitudeReferenceFrame)referenceFrame

	1、开始加速度计/陀螺仪/磁力计/运动方向更新，但是没有处理的block
	2、可以通过accelerometerData的属性来获得最近一次更新
	3、不再需要更新数据的时候，应该调用stopAccelerometerUpdates
	4、device motion使用attitudeReferenceFrame返回的坐标系
	5、device motion usingReferenceFrame可以指定坐标系，其他都和startDeviceMotionUpdates相同
	
–(void)stopAccelerometerUpdates

–(void)stopGyroUpdates

–(void)stopMagnetometerUpdates

-(void)stopDeviceMotionUpdates
 
	停止加速度计/陀螺仪/磁力计/运动方向更新


#####判断加速度计/陀螺仪/磁力计状态

@property(readonly, nonatomic, getter=isAccelerometerActive) BOOL accelerometerActive

@property(readonly, nonatomic, getter=isGyroActive) BOOL gyroActive

@property(readonly, nonatomic, getter=isMagnetometerActive) BOOL magnetometerActive

@property(readonly, nonatomic, getter=isDeviceMotionActive) BOOL deviceMotionActive

	判断加速度计/陀螺仪/磁力计/运动方向是否处于激活状态（即调用了开始且没有调用暂停）

@property(readonly, nonatomic, getter=isAccelerometerAvailable) BOOL accelerometerAvailable

@property(readonly, nonatomic, getter=isGyroAvailable) BOOL gyroAvailable

@property(readonly, nonatomic, getter=isMagnetometerAvailable) BOOL magnetometerAvailable


@property(readonly, nonatomic, getter=isDeviceMotionAvailable) BOOL deviceMotionAvailable

	1、判断加速度计/陀螺仪/磁力计/运动方向在设备上是否可用
	2、deviceMotion需要判断加速度计和陀螺仪都可用，但是因为所有的设备都有加速度计，于是这个属性等价于gyroAvailable
	
#####访问加速度计/陀螺仪/磁力计/运动方向数据
 
@property(readonly) CMAccelerometerData *accelerometerData

@property(readonly) CMGyroData *gyroData

@property(readonly) CMMagnetometerData *magnetometerData

@property(readonly) CMDeviceMotion *deviceMotion

	如果加速度计/陀螺仪/磁力计/运动方向数据不可用，则这个属性返回nil。
	
	在调用startAccelerometerUpdates(startGyroUpdates / startMagnetometerUpdates / startDeviceMotionUpdates)之后这个属性会有值，可以周期性的访问这个属性来获得最新数据
	
	1、CMAccelerometerData 
		@property(readonly, nonatomic) CMAcceleration acceleration 加速度
		CMAcceleration 是一个结构体，double x,y,z(三个轴在重力下的加速度)
	2、CMGyroData 
		@property(readonly, nonatomic) CMRotationRate rotationRate 旋转弧度
		CMRotationRate 是一个结构体，double x,y,z（三个轴的旋转弧度）
	3、CMMagnetometerData
		@property(readonly, nonatomic) CMMagneticField magneticField 磁力域
		CMMagneticField 是一个结构体，double x,y,z(三个轴的磁场)
	4、CMDeviceMotion
		@property(readonly, nonatomic) CMAttitude *attitude 设备方向			参数 pitch yaw roll （绕x,y,z旋转）
			参数CMRotationMatrix rotationMatrix 旋转矩阵
				结构是 double m11, m12, m13
			   		  double m21, m22, m23
			   		  double m31, m32, m33
			参数 CMQuaternion quaternion 代表设备方向的四元数
				结构是 double x,y,z,w（四个轴）
				四元数将三维中旋转的概念扩展到四维中的旋转。表示可在一个对象的两个方向之间插入的最			有效的旋转。
				四元数在定义一个向量的 [x, y, z] 值中添加第四个分量，生成任意的四维向量。然而，			下面的公式说明单位四元数的每个分量与轴角度旋转之间的关系，其中，q 表示一个单位四元数 			(x, y, z, w)，轴经过正规化，theta 为要绕轴进行逆时针 (CCW) 旋转的角度。
		
		@property(readonly, nonatomic) CMAcceleration gravity 重力加速度
			设备的全部加速度等同于重力加上用户作用于设备的加速度
		@property(readonly, nonatomic) CMCalibratedMagneticField magneticField 磁场
			这个值返回的是设备附近没有偏差的全部磁场域，不像是CMMagnetometer中的				magneticField，那个值是地球磁场域 + 周边磁场域 - 设备偏差
			CMCalibraredMagneticField 是一个结构体
				CMMagneticField field
				CMMagneticFieldCalibrationAccuracy accuracy。
			如果设备没有磁力仪，这个值会返回CMMagneticFieldCalibrationAccuracyUncalibrated
		@property(readonly, nonatomic) CMRotationRate rotationRate 旋转角度
		@property(readonly, nonatomic) CMAcceleration userAcceleration 用户加速度
	5、CMLogItem 这些类的父类
		@property(readonly, nonatomic) NSTimeInterval timestamp 被记录的数据有效的时间
	
#####访问坐标系

@property(readonly, nonatomic) CMAttitudeReferenceFrame attitudeReferenceFrame

	如果运动方向现在是激活状态的，则这个属性返回的是当前使用的，如果没有激活但是曾经激活过，那么返回的是之前用过的坐标系，如果从app运行之后从未激活，则返回默认的坐标系。如果运动方向在这个设备上不可用，则返回值未定义。
	
+(NSUInteger)availableAttitudeReferenceFrames

	返回可用的坐标系的位掩码
	
	用枚举来判断某个坐标系是否可用
	
	例如：
	if ([CMMotionManager availableAttitudeReferenceFrames] & 		CMAttitudeReferenceFrameXMagneticNorthZVertical) {
    	// do something appropriate here
	}
	
	CMAttitudeReferenceFrame枚举类型说明	
	   	CMAttitudeReferenceFrameXArbitraryZVertical = 1 << 0,
   		CMAttitudeReferenceFrameXArbitraryCorrectedZVertical = 1 << 1,
   		CMAttitudeReferenceFrameXMagneticNorthZVertical = 1 << 2,
   		CMAttitudeReferenceFrameXTrueNorthZVertical = 1 << 3

	
###CMMotionActivityManager
提供访问存储在设备中的运动数据
判断用户状态（静止、步行、跑步、车上）
导航APP可以通过用户状态的改变提供不同方向的指引
#####确定服务是否可用

+(BOOL)isActivityAvailable 确定是否可用
	
	只支持5s,因为有M7处理器
	
#####开始/停止更新
-(void)startActivityUpdatesToQueue:(NSOperationQueue *)queue 
withHandler:(CMMotionActivityHandler)handler 开启更新
	
	如果程序被挂起，将不会调用更新，最后一次更新将会在程序苏醒之后调用
	要得到全部更新，只能通过查询语句查询挂起时的更新情况

–(void)stopActivityUpdates   停止更新
	
	会把开启更新给停止，但是不会停止已经开始的查询
	
#####获取历史数据
-(void)queryActivityStartingFromDate:(NSDate *)start toDate:(NSDate *)end 
toQueue:(NSOperationQueue *)queue withHandler:(CMMotionActivityQueryHandler)handler  （查询历史数据）
	
	start 查询的开始时间 end 查询的结束时间 queue 做这个操作的线程（主线程亦可） handler 查询结果
	这四个参数都不能为空
	
	CMMotionActivityQueryHandler  这个block有两个参数NSArray *activities 和NSError *error
	 
	activities这个数组存储的是CMMotionActivity类型的对象，通过对象的startDate可以查询每次更新的时间
	
	数组按照时间排序

		CMMotionActivity 包含相关的运动数据，其中的判断不是互相独立的，换言之可能多个属性被设置为YES

		例如开车的时候遇到红灯停下来了，这时候automotive和stationary都会被设为YES,当设备在运动中但是运动和步行、跑步、汽车都无关的时候，可能所有的属性都会设为NO
		不能自己创建实例对象 CMMotionActivityManager会创建并发送给注册的操作块。
  			stationary 设备是否静止（只读） 
   			walking  
   			running 用户是否在跑步（只读）
   			automotive 判断是否在车里（只读）
   			unknown 
   			startDate 运动发生时的时间（只读）
   			confidence 判断这个运动类型是否精确的信心（只读）枚举Low Medium High三类



###CMStepCouter
#####确定服务是否可用
+(BOOL)isStepCountingAvailable

	只支持5s,因为有M7处理器
	
#####获取历史数据
-(void)queryStepCountStartingFrom:(NSDate *)start to:(NSDate *)end toQueue:(NSOperationQueue *)queue withHandler:(CMStepQueryHandler)handler

#####开始/停止更新
-(void)startStepCountingUpdatesToQueue:(NSOperationQueue *)queue updateOn:(NSInteger)stepCounts withHandler:(CMStepUpdateHandler)handler

	如果程序被挂起，将不会调用更新，最后一次更新将会在程序苏醒之后调用
	要得到全部更新，只能通过查询语句查询挂起时的更新情况
	
	stepCounts是开始调用之后的全部步数
	
	
-(void)stopStepCountingUpdates
	
	会把开启更新给停止，但是不会停止已经开始的查询

