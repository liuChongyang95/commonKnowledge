Service ��Ҫԭ�� 1.�򻯺�̨�����ʵ��
                 2.ʵ��ͬһ̨�豸���п���̵�Զ��ͨ��

Local Service & Remote Service ���غ�Զ��

���� ֧��ͬһ�����ڵ�Ӧ�ó�����з���
Զ�� ����ͨ��AIDL����֧�ֿ���̷��� 

��������ͨ�� Context.startService()�����ط���
             Context.bindService()�����ط���Զ�̷���

----
1.1 ���壺�ṩ����֧�֣�������м���
ʵ��������λ�ü�⡢SD��ɨ�衢���������ڼ�⡣

*Ҫ����첽����

----
1.2 �������ͣ�

1.2.1
    ��������ģ�ͷ��ࣺContext.startService()������Context.stopService()������ȱ������ԣ�

                      Context.bindService()������Context.unbindService()��������ͨ��Ibinder����л�ȡService�ľ����

startService()�������ط���,bindService()����Զ�̰�.Ҳ���Ի��ʹ�ã���ΰ󶨡�

1.2.2
    ���Ĵ淽ʽ����:���ط��� 
                   �Ĵ��ڵ�ǰ�����У���ǰ���̽���Service������
                   �����Զ������̣߳���Ҫ�˹�������֮��Serivice���Ĵ������̡߳�
 
                   Զ�̷��� 
                   �Ĵ�����һ�����̣�ͨ��AIDL��android interface definition language������ӿ����ԣ�
                   ʵ��Android�豸���������̼�ͨ�ţ�IPC����
                   AIDL��IPC���ƻ���RPC��Remote process call��Զ�̹��̵���Э�齨���ģ�����Լ�����̼��ͨѶ���򣬹����������ɴ��롣
    
----
Service����������

����                                      ˵��

void onCreate����                         ��Service������ʱ��������������������ֻ����һ�Ρ�


int onStartCommand(Intent intent,         ͨ��Context.startService��������ʱ������
int flags,int startId)                    intent ��startCommand���������flags��������ʽ��startId��Ψһ��־��������ֵ���������Ĵ���ʽ

void onStart��Intent intent,int startId�� ������onStartCommand
 
IBinder onBind(Intent intent)             Context.bindService����������һ��IBinder����������Զ�̷���ʱ��Service����Զ�̲ٿ�
                  
void onRebind��Intent intent��            ����������startService��bindService��������onUnbind����trueʱ���´�bindService��������

boolean onUnbind(Intent intent)           ����Context.unbindService������Ĭ�Ϸ���false������true���ٴε���Context.bindService������onRebind

void onDestroy()                          1.startService��stopService 2.bindService��bindService 3. startService+bindService��unbindService+stopService
                                          (sS��bS˭��˭������ν)
----

onStartCommand����

Service��kill��Ĵ���ʽ:int onStartCommand�ķ���ֵ

START_STICKY
���Service��kill��ϵͳ�᳢�����´��������û���κ�����������ݵ�Service��intent��Ϊnull��

START_NOT_STICKY
ʹ���������ֵ�������ִ����onStartCommand�����󣬷����쳣kill��ϵͳ���������÷���

START_REDELIVER_INTENT
ʹ���������ֵ�������ִ����onStartCommand�����󣬷����쳣kill��ϵͳ���Զ������÷��񣬲���intent��ֵ���롣

START_STICKY_COMPATIBILITY
START_STICKY�ļ��ݰ�,������֤����kill��һ����������
�������flags����˴�onStartCommand��������ʽ������������ֵΪ0;kill������������������� START_FLAG_RETRY �����ϴη���START_STICKY,���Բ���intent Ϊ null��
                                                                                        START_FLAG_REDELIVERY ���ڷ���ֵΪSTART_REDELIVER_INTENT,���Դ��������intent��

----
2.2 Service����������

Context.startService��intent������ʱ���ȴ���Service��onCreate()�����г�ʼ������������������ֻ����һ�Ρ�
                                      Ȼ�󴥷�Service��onStartCommand()������ÿ�ε���startService������á�
                                      ֮��Service ��������Դ���������±�ϵͳ kill ��������Service�����Զ�������
                                      ֱ��ϵͳ����Context.stopService()����ʱ��Service �Ż������
                                      ��Service����ʱ���Զ�����onDestory()��������ת�е�Service�������

Context.bindService()��������ʱ��Ҳ�ᴥ��onCreate��Ȼ�󴥷�onBind�Է�����а󶨣��ɹ���ȡService�����ϵͳ��ͨ��
                                 �û��Զ����serviceConnection����onServiceConnected��ComponentName name��IBinder service������
                                 ��Service���������������ϵͳ����unbindServiceʱ���ͻἤ��onDestory�������
----
Service����˵����
android:name��       ����������ע�����Service��Activity����ͬһ�����У���android:name�ϱ���д��Service��ȫ·��
android:label����    ��������֣����Ϊ�գ�Ĭ����ʾ�ķ�����Ϊ����
android:icon����     �����ͼ��
android:permission   �����˷����Ȩ�ޣ�����ζ��ֻ���ṩ�˸�Ȩ�޵�Ӧ�ò��ܿ��ƻ����Ӵ˷���
android:process��    ��ʾ�÷����Ƿ�����������һ�����̣���������˴����ô�����ڰ��������������ַ�����ʾ��һ���̵�����
android:enabled��    �����������Ϊ true����ô Service ����Ĭ�ϱ�ϵͳ������Ĭ��ֵΪ false
android:exported��   ��ʾ�÷����Ƿ��ܹ�������Ӧ�ó��������ƻ����ӣ�Ĭ��ֵΪ false
----
3.1 ͨ��Context.bindService����Service����

IBinder��BinderԶ�̶���Ļ����ӿڣ�����ӿڶ�������Զ�̶���Ľ���Э�飬������������Զ�̵��ã�Ҳ���ڽ����ڵ��á�
ϵͳ����ͨ��IBinder��ȡService�ľ����
ServiceConnection��Ҫ����ͨ��Binder��Service����󣬶�Service������д�������Ҫ����������
void onServiceConnected(ComponentName name,IBinder service)��
void onServiceDisconnected(ComponentName name)��
��Context.bindService()��ɰ󶨺�ϵͳ�ͻ����onServiceConnected()�������û�����ͨ��IBinder������ȡService�����
��Service���д�����onServiceDisconnected()����һ�㲻����ã�ֻ��Service���󶨺������ڴ治������ⱻkill�Ż���á�
----
3.3 Service������ۺ�����

Ŀǰ������ǽ��startService()+bindService()���ַ�ʽ����Service����
    startService()�������Service����������������ʼ��������
    bindService()����ʱ��Service������м�⡣
�����ǹ��������̣���startService()���������ÿʹ��bindService()�󶨷��񣬾�ͨ��serviceConnection�Է�����м�⣬
Ȼ����unbindService()�����󶨡���ʱ����δ���������ǳ��������ں�̨��ֱ��ϵͳ��stopService()�������������,Service�Ż�������ᡣ

ͨ��startService()��������󣬶��ʹ��bindService()�󶨷���,unbindService()����󶨣����ͨ��stopService()�����󣺽������
onBind����������onUnbind��������ֻ�ڵ�һ��bindService�����д���������ε���bindService()�����¼������ᱻ������
��ֻ�ᴥ��onServiceConnected()�� ��ΪĬ������£�ϵͳ�ڰ�ʱ��������IBinder�ӿڣ����Service�Ѿ�����Binder����
ϵͳ�ͻ�ֱ������onBind()������

����ͨ��void onRebind(intent)������Service������boolean onUnbind��intent����Ĭ�Ϸ���ֵΪfalse����Ϊtrue��
��ô���ڵڶ��ε���Context.bindService()��ʱ�򣬾ͻἤ��Service.onRebind(intent)��ȥ�л���ͬ�İ󶨡�

----
4.1��Runnable�ӿ�ʵ��Service���̲߳���

����Androidϵͳ��Դ���ޡ�GPU��RAM��CPU���и������л��ơ�
�����߳��д��ڴ��ļ���ȡ��ͼƬ���������������ӳ�ʱ�Ȳ���ʱ��
һ��ʱ�䳬��5�룬Androidϵͳ�ͻ���֡��������л���������ʾ��
logcat��־��Ҳ����ʾ��The application may be doing too work on its main thread������ʾ��
�ڿ���Service����ʱ�������ڴ������ʱ��������Ա��Ӧ�ó���ʹ�ö��̷߳�ʽ���п������������̱߳���ʱ��ռ�á�

ͼƬ

----
4.2 IntentService������
��Service�������ĳ�����ʱ�Բ������ձ������������
��AndroidϵͳΪ������Ա�ṩ��Service������IntentService����IntentServiceִ��startService()����ʱ��
ϵͳ��ʹ��һ��ѭ�����򽫸÷�����뵽һ�����̶߳��е��У��Ա�ִ�з����еĲ�����

public abstract class IntentService extends Service {
    private volatile Looper mServiceLooper;
    private volatile ServiceHandler mServiceHandler;
    private String mName;
    private boolean mRedelivery;

    private final class ServiceHandler extends Handler {
        public ServiceHandler(Looper looper) {
            super(looper);
        }

        @Override
        public void handleMessage(Message msg) {
            onHandleIntent((Intent)msg.obj);
            stopSelf(msg.arg1);
        }
    }

    public IntentService(String name) {
        super();
        mName = name;
    }

    public void setIntentRedelivery(boolean enabled) {
        mRedelivery = enabled;
    }

    @Override
    public void onCreate() {
        super.onCreate();
        HandlerThread thread = new HandlerThread("IntentService[" + mName + "]");
        thread.start();

        mServiceLooper = thread.getLooper();
        mServiceHandler = new ServiceHandler(mServiceLooper);
    }

    @Override
    public void onStart(Intent intent, int startId) {
        Message msg = mServiceHandler.obtainMessage();
        msg.arg1 = startId;
        msg.obj = intent;
        mServiceHandler.sendMessage(msg);
    }

    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        onStart(intent, startId);
        return mRedelivery ? START_REDELIVER_INTENT : START_NOT_STICKY;
    }

    @Override
    public void onDestroy() {
        mServiceLooper.quit();
    }

    @Override
    public IBinder onBind(Intent intent) {
        return null;
    }

    protected abstract void onHandleIntent(Intent intent);
}

��onCreate()�����н����˶����Ĺ����̣߳��ڳ�ʼ��ʱ�������߳�ȥִ�ж���첽����
��ϵͳ����Context.startService()����ʱ����ͨ��onStart()����ʹ���첽��ʽ������ServiceHandler.handlerMessage(msg)
���д�����handleMessage��msg���������ⷽ��onHandleIntent��Intent����Ȼ����stopSelf()��������
������Ҫ��дHandleIntent(Intent)����������첽����ִ��IntentService��
----

�塢Remote Serviceԭ��

5.1 �����ͨ�ŵ�ʹ�ó���

���϶���LocalService������Service�������Client�ͻ��˶�����ͬһ���̵��У���App��ж�أ�Service����Ҳ��ͬʱж�ء�
����ѷ������ͻ��˷ֱ���ڲ�ͬ�Ľ��̵��н��п������Ϣ��������Ҫ�õ�Զ��ͨ�ŷ���Remote Service��
remoteService���԰ѷ������ͻ��˷��룬һ����ж�أ���һ�����ᱻӰ�졣
���App�Ĺ������û���Ϣ�������֤�ȶ������ģ�鶼������Service������ʵ�֣��Թ���ͬ��App���е��á�
���ҵ�App���ر�ʱ��Service���񻹻�Ĵ��ں�̨���У����û��������м�⡣
----
5.2 Remote Service��������

��ͬApp���ڲ�ͬ����Process��һ�����̲���ֱ�ӷ����������̵���Դ����Ҫʵ�ֶ����֮���ͨ�ţ���Ҫ����IPC���̼�ͨ�ż�����
android IPC����RPCԶ�̹��̵���Э�齨���ģ�ϵͳ�����AIDL���ӿڶ������ԣ��������Ϣ�������л�����Ȼ���͵���һ�����̵��С�
���ֻ��ڿ����ͨ�ŵķ������Remote Service��
----
5.3 IPC����ԭ��

�ӵײ�ܹ�������Androidϵͳ��IPC��������Ҫ�����롰ServiceManager���͡�Binder Driver����������Ԫ����

ServiceManager���

ServiceManager��Androidϵͳ�ڵķ������������Ҫ�������Service����Ĺ���ע�ᣬ���õ�����

ServiceManager������ͨ��binder_loopѭ����Binder Driver���м����������������µ�Service��������󣬾ͻ����
svcmgr_handler()�����Լ���Service������д���ͨ��*do_find_service()����������svclist���м��Service����
����ǰsvclist������δ���ڵ�ǰ���񣬾ͻ�ͨ��do_add_service()����ע�ᣬ�ѵ�ǰ������Ψһ��־�����뵽svclist�У�
������ǰ��Service���񱻰󶨺�������ServiceManager��ע�ᡣ

Binder Driver�ᰴ�չ涨�ĸ�ʽ�ѵ�ǰServiceת��ΪBinderʵ�巢�͵��ں˵��У�����Client����ʱ
ServiceManager�����Service����ı�ʶ����svclist���ҵ���Binderʵ�壬����Binderʵ������÷��͸�Client��
��ɼ����Binder Driver��������ݴ������Ѽ��������ص�Client�ͻ��ˡ�
����Binderʵ������ǿ���͵���ʽ���ڣ����Լ�ʹ��������ã�ϵͳ����ָ��ͬһ��Binderʵ�壬�������ж��������ӣ�
����Binderʵ��һֱ���ڡ�

ͼƬ

Binder Driver���

Binder Driver������Android�ں˵��У����ԡ��ַ������豸���еġ�misc�豸ע�ᡱ�������豸Ŀ¼dev/binder��
�������֮��Binderͨ�ŵĽ�����Binderʵ���ڽ���֮��Ĵ��ݣ�Binderʵ�����õļ����������ݰ��ڽ���֮��Ĵ�����
������һϵ�еײ������
----
5.4 Remote Service���ýӿ�

IBinder�ӿ�
IBinder��Remote ServiceԶ�̷���ĳ��ýӿڣ�Binder������ʵ���ࡣ
IBinder�ڲ��Ƚ���Ҫ�ķ�������boolean transact(int code��Parcel data��Parcel reply��int flags)��
�������������ͻ���֮�������Ϣ����������Զ�̷������д������ѷ���ֵת���ɿ����л������ͻؿͻ��ˡ�













ConstraintLayout �ʺ���ק��������