# DeviceOwnerDemo
MDM device Admin &amp; device owner Demo


Device Owner
����
DeviceOwner ��Ϊ�豸�����ߣ���Android5.0ϵͳ�Ƴ���DeviceOwner������DeviceAdmin�û������й���������Ҳ������ProfileOwner�����й�����������������Щ�����϶��������һЩ����Ȩ�ޣ��������豸������״̬���ȡ�Android�ṩ������Ȩ�޹�����Ե�������С����Ϊ DeviceAdmin < ProfileOwner < DeviceOwner��

Androidϵͳֻ������һ��DeviceOwner���򣬲��Ҹó���������ΪDeviceOwner����ȡ����Ӧ�ò���ж�أ�Ψһ����ȡ����;���ǻָ��������á����ң�DeviceOwnerӦ�ú�ProfileOwnerҲ�������ͻ��ϵͳֻ����һ��DeviceOwnerӦ�û���ProfileOwnerӦ�á�

DeviceOwner �����ú�����
Ҫʹһ��Ӧ�ó�ΪDeviceOwner������������������һ��DeviceAdmin������DeviceAdmin�ı�׼��������һ�����򣬻ع���������Android Device Administration Ӧ�õ�������
�����úõĳ�������ΪDeviceOwner֮ǰ�����ؿ���ȥ����DeviceAdmin��ϵͳ������DeviceOwner�Ĺ����л��Զ��ȼ���DeviceAdmin����Ҳ��DeviceOwnerӵ��DeviceAdmin����������ԭ��
������Ӧ�ú�ϵͳӦ�ö�û��Ȩ������DeviceOwner��Android�ٷ�ֵ�ṩ��������DeviceOwnerӦ�õķ�����

ͨ���ն�adb shell
ͨ��NFC
�˽�ٷ��������Զ���ʵ�ַ���������ת��һ������ DeviceAdmin/ProfileOwner/DeviceOwner Ӧ��

ϵͳ�ɹ�����DeviceOwner�������/data/system/device_owner_2.xml �ļ������ļ���¼��ϵͳ��߹���Ȩ�޳���Ļ�����Ϣ��

<?xml version='1.0' encoding='utf-8' standalone='yes' ?>
<root>
<device-owner package="com.action.deviceadmin" name="Test Device Owner" component="com.action.deviceadmin/com.action.deviceadmin.DPMTestReceiver" userRestrictionsMigrated="true" />
<device-owner-context userId="0" />
</root>
1
2
3
4
5
�Ƿ�ΪDeviceOwner
// ��ȡ�豸�������
mDevicePolicyManager = (DevicePolicyManager) getSystemService(Context.DEVICE_POLICY_SERVICE);
// ��Ҫ�����DeviceAdminReceiver���
mComponentName = new ComponentName(this, DPMTestReceiver.class);

isDeviceOwnerApp = mDevicePolicyManager.isDeviceOwnerApp(mComponentName.getPackageName());
Log.d(TAG, "isDeviceOwnerApp: " + isDeviceOwnerApp);
1
2
3
4
5
6
7
���û���ñ��ݷ���
private void setBackupServiceEnabled(ComponentName admin, boolean enabled) {
	    if (isDeviceOwnerApp) {
	        mDevicePolicyManager.setBackupServiceEnabled(admin, enabled);
	    }
	}
1
2
3
4
5
���ݷ����Ƿ���
private boolean isBackupServiceEnabled(ComponentName admin) {
	    boolean res = false;
	    if (isDeviceOwnerApp) {
	        res = mDevicePolicyManager.isBackupServiceEnabled(admin);
	    }
	    return res;
	}
1
2
3
4
5
6
7
�����豸
private void reboot(ComponentName admin) {
	    if (isDeviceOwnerApp) {
	        mDevicePolicyManager.reboot(admin);
	    }
	}
1
2
3
4
5
��ȡwifi Mac��ַ
private String getWifiMacAddress(ComponentName admin) {
	    String res = null;
	    if (isDeviceOwnerApp) {
	        res = mDevicePolicyManager.getWifiMacAddress(admin);
	    }
	    return res;
	}
1
2
3
4
5
6
7
����״̬���Ľ��û�����
private boolean setStatusBarDisabled(ComponentName admin, boolean disabled) {
	    boolean res = false;
	    if (isDeviceOwnerApp) {
	        res = mDevicePolicyManager.setStatusBarDisabled(admin, disabled);
	    }
	    return res;
	}
1
2
3
4
5
6
7
������ģʽ����ΪNone�����û�����������ʱ��Ч
private boolean setKeyguardDisabled(ComponentName admin, boolean disabled) {
	    boolean res = false;
	    if (isDeviceOwnerApp) {
	        res = mDevicePolicyManager.setKeyguardDisabled(admin, disabled);
	    }
	    return res;
	}
1
2
3
4
5
6
7
����ϵͳ���²���
private void setSystemUpdatePolicy(ComponentName admin, SystemUpdatePolicy policy) {
	    if (isDeviceOwnerApp) {
	        mDevicePolicyManager.setSystemUpdatePolicy(admin, policy);
	    }
	}
1
2
3
4
5
��ȡϵͳ���²���
private SystemUpdatePolicy getSystemUpdatePolicy() {
	    SystemUpdatePolicy res = null;
	    if (isDeviceOwnerApp) {
	        res = mDevicePolicyManager.getSystemUpdatePolicy();
	    }
	    return res;
	}
1
2
3
4
5
6
7
����ϵͳ������Global��ص�����
private void setGlobalSetting(ComponentName admin, String setting, String value) {
	    if (isDeviceOwnerApp) {
	        mDevicePolicyManager.setGlobalSetting(admin, setting, value);
	    }
	}
1
2
3
4
5
�л��û�
private boolean switchUser(ComponentName admin, UserHandle userHandle) {
	    boolean res = false;
	    if (isDeviceOwnerApp) {
	        res = mDevicePolicyManager.switchUser(admin, userHandle);
	    }
	    return res;
	}
1
2
3
4
5
6
7
ɾ���û�
private boolean removeUser(ComponentName admin, UserHandle userHandle) {
	    boolean res = false;
	    if (isDeviceOwnerApp) {
	        res = mDevicePolicyManager.removeUser(admin, userHandle);
	    }
	    return res;
	}
1
2
3
4
5
6
7
����һ���û�
private UserHandle createAndManageUser(ComponentName admin, String name, ComponentName profileOwner, PersistableBundle adminExtras,
            int flags) {
	    UserHandle res = null;
	    if (isDeviceOwnerApp) {
	        res = mDevicePolicyManager.createAndManageUser(admin, name, profileOwner, adminExtras, flags);
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
��������������ʾ����ʾ��Ϣ�C�硰С����Device Owner�豸��
private void setDeviceOwnerLockScreenInfo(ComponentName admin, CharSequence info) {
	    if (isDeviceOwnerApp) {
	        mDevicePolicyManager.setDeviceOwnerLockScreenInfo(admin, info);
	    }
	}
1
2
3
4
5
��ȡ����������ʾ��Ϣ
private CharSequence getDeviceOwnerLockScreenInfo() {
	    CharSequence res = null;

	    if (isDeviceOwnerApp) {
	        res = mDevicePolicyManager.getDeviceOwnerLockScreenInfo();
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
����һ�������������ȫ��HTTP����
private void setRecommendedGlobalProxy(ComponentName admin, ProxyInfo proxyInfo) {
	    if (isDeviceOwnerApp) {
	        mDevicePolicyManager.setRecommendedGlobalProxy(admin, proxyInfo);
	    }
	}
1
2
3
4
5
��ֹ/�������
private void setScreenCaptureDisabled(ComponentName admin, boolean disabled) {
        if(isProfileOwnerApp) {
	        mDevicePolicyManager.setScreenCaptureDisabled(admin, disabled);
	    }
    }
1
2
3
4
5
�Ƿ��ֹ��ͼ
private boolean getScreenCaptureDisabled(ComponentName admin) {
	    boolean res = false;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.getScreenCaptureDisabled(admin);
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
������֯��
private void setOrganizationName(ComponentName admin, CharSequence title) {
	    if(isProfileOwnerApp) {
	        mDevicePolicyManager.setOrganizationName(admin, title);
	    }
	}
1
2
3
4
5
��ȡ��֯��
private CharSequence getOrganizationName(ComponentName admin) {
	    CharSequence res = null;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.getOrganizationName(admin);
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
ͨ����������Ӧ�ó��������ʱȨ��״̬
private boolean setPermissionGrantState(ComponentName admin, String packageName,
            String permission, int grantState) {
	    boolean res = false;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.setPermissionGrantState(admin, packageName, permission, grantState);
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
9
ͨ��������ȡӦ�ó��������ʱȨ��״̬
private int getPermissionGrantState(ComponentName admin, String packageName,
            String permission) {
	    int res = 0;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.getPermissionGrantState(admin, packageName, permission);
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
9
����Ӧ�ó����Զ������ܾ�����ʱȨ������
private void setPermissionPolicy(ComponentName admin, int policy) {
	    if(isProfileOwnerApp) {
	        mDevicePolicyManager.setPermissionPolicy(admin, policy);
	    }
	}
1
2
3
4
5
�����豸�������ļ����������õĵ�ǰ����ʱȨ�޲���
private int getPermissionPolicy(ComponentName admin) {
	    int res = 0;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.getPermissionPolicy(admin);
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
�����û�ͼƬ
private void setUserIcon(ComponentName admin, Bitmap icon) {
	    if(isProfileOwnerApp) {
	        mDevicePolicyManager.setUserIcon(admin, icon);
	    }
	}
1
2
3
4
5
����Ӧ�ó��򲻿�ж�ػ��߿���ж��
private void setUninstallBlocked(ComponentName admin, String packageName,
            boolean uninstallBlocked) {
	    if(isProfileOwnerApp) {
	        mDevicePolicyManager.setUninstallBlocked(admin, packageName, uninstallBlocked);
	    }
	}
1
2
3
4
5
6
����Ӧ�ó����Ƿ��ж��
private boolean isUninstallBlocked(ComponentName admin, String packageName) {
	    boolean res = false;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.isUninstallBlocked(admin, packageName);
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
���þ���
private void setMasterVolumeMuted(ComponentName admin, boolean on) {
	    if(isProfileOwnerApp) {
	        mDevicePolicyManager.setMasterVolumeMuted(admin, on);
	    }
	}
1
2
3
4
5
�Ƿ���
private boolean isMasterVolumeMuted(ComponentName admin) {
	    boolean res = false;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.isMasterVolumeMuted(admin);
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
ָ���ض��ķ��������Ϊ�����ṩ�ߣ��������û��ı��ػ�Զ�̹���Ա����Ȩ������
private void setRestrictionsProvider(ComponentName admin, ComponentName provider) {
	    if(isProfileOwnerApp) {
	        mDevicePolicyManager.setRestrictionsProvider(admin, provider);
	    }
	}
1
2
3
4
5
����ϵͳ�����а�ȫ��ص�����
private void setSecureSetting(ComponentName admin, String setting, String value) {
	    if(isProfileOwnerApp) {
	        mDevicePolicyManager.setSecureSetting(admin, setting, value);
	    }
	}
1
2
3
4
5
������ЩӦ�ó����ܹ�������������ʾ
private void setLockTaskPackages(ComponentName admin, String[] packages) {
	    if (packages == null) return;

	    if(isProfileOwnerApp) {
	        mDevicePolicyManager.setLockTaskPackages(admin, packages);
	    }
	}
1
2
3
4
5
6
7
��������������������ʾ�İ��б�
private String[] getLockTaskPackages(ComponentName admin) {
	    String[] res = null;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.getLockTaskPackages(admin);
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
��ѯһ��Ӧ���Ƿ��ܹ�������������ʾ
private boolean isLockTaskPermitted(String packageName) {
	    boolean res = false;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.isLockTaskPermitted(packageName);
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
�����ض����͵��ʻ�
private void setAccountManagementDisabled(ComponentName admin, String accountType,
            boolean disabled) {
	    if(isProfileOwnerApp) {
	        mDevicePolicyManager.setAccountManagementDisabled(admin, accountType, disabled);
	    }
	}
1
2
3
4
5
6
��ȡ���õ��˻��б�
private String[] getAccountTypesWithManagementDisabled() {
	    String[] res = null;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.getAccountTypesWithManagementDisabled();
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
���������û���ʼ��ʱĬ�Ͻ��õ�ϵͳӦ�ó���
private void enableSystemApp(ComponentName admin, String packageName) {
	    if(isProfileOwnerApp) {
	        mDevicePolicyManager.enableSystemApp(admin, packageName);
	    }
	}
1
2
3
4
5
���ػ�������Ӧ��
private boolean setApplicationHidden(ComponentName admin, String packageName, boolean hidden) {
	    boolean res = false;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.setApplicationHidden(admin, packageName, hidden);
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
��ѯһ��Ӧ���Ƿ�����
private boolean isApplicationHidden(ComponentName admin, String packageName) {
	    boolean res = false;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.isApplicationHidden(admin, packageName);
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
����û�����
private void addUserRestriction(ComponentName admin, String key) {
	    if(isProfileOwnerApp) {
	        mDevicePolicyManager.addUserRestriction(admin, key);
	    }
	}
1
2
3
4
5
����û�����
private void clearUserRestriction(ComponentName admin, String key) {
	    if(isProfileOwnerApp) {
	        mDevicePolicyManager.clearUserRestriction(admin, key);
	    }
	}
1
2
3
4
5
��ȡ�û�����
private Bundle getUserRestrictions(ComponentName admin) {
	    Bundle res = null;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.getUserRestrictions(admin);
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
Ĭ������£��û�����ʹ���κ����뷨������������������ʱ���û��޷����ò����б��е����뷨
private boolean setPermittedInputMethods(ComponentName admin, List<String> packageNames) {
	    boolean res = false;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.setPermittedInputMethods(admin, packageNames);
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
��ȡ�����ε����뷨���б�
private List<String> getPermittedInputMethods(ComponentName admin) {
	    List<String> res = null;
	    if(isProfileOwnerApp) {
	        res = mDevicePolicyManager.getPermittedInputMethods(admin);
	    }
	    return res;
	}
1
2
3
4
5
6
7
��������Ŀɷ����Է���Ĭ������£��û�����ʹ���κοɷ����Է��񡣵���������������ʱ���û��޷������б��з�ϵͳ���ֵĿɷ����Է���
private boolean setPermittedAccessibilityServices(ComponentName admin, List<String> packageNames) {
	    boolean res = false;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.setPermittedAccessibilityServices(admin, packageNames);
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
��ȡ���в������εķ����б�
private List<String> getPermittedAccessibilityServices(ComponentName admin) {
	    List<String> res = null;
	    if(isProfileOwnerApp) {
	        res = mDevicePolicyManager.getPermittedAccessibilityServices(admin);
	    }
	    return res;
	}
1
2
3
4
5
6
7
���������Ƿ���Է�����ϵ��
private void setBluetoothContactSharingDisabled(ComponentName admin, boolean disabled) {
	    if(isProfileOwnerApp) {
	        mDevicePolicyManager.setBluetoothContactSharingDisabled(admin, disabled);
	    }
	}
1
2
3
4
5
��ȡ����������ϵ��״̬
private boolean getBluetoothContactSharingDisabled(ComponentName admin) {
	    boolean res = false;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.getBluetoothContactSharingDisabled(admin);
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
��ֹ���߿���������ϵ�˹���
private void setCrossProfileContactsSearchDisabled(ComponentName admin, boolean disabled) {
	    if(isProfileOwnerApp) {
	        mDevicePolicyManager.setCrossProfileContactsSearchDisabled(admin, disabled);
	    }
	}
1
2
3
4
5
��ȡ������ϵ��״̬
private boolean getCrossProfileContactsSearchDisabled(ComponentName admin) {
	    boolean res = false;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.getCrossProfileContactsSearchDisabled(admin);
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
��ֹ���߿���������ʾ����
private void setCrossProfileCallerIdDisabled(ComponentName admin, boolean disabled) {
	    if(isProfileOwnerApp) {
	        mDevicePolicyManager.setCrossProfileCallerIdDisabled(admin, disabled);
	    }
	}
1
2
3
4
5
��ȡ��ֹ������ʾ״̬
private boolean getCrossProfileCallerIdDisabled(ComponentName admin) {
	    boolean res = false;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.getCrossProfileCallerIdDisabled(admin);
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
����Ӧ������
private void setApplicationRestrictions(ComponentName admin, String packageName,
            Bundle settings) {
	    if(isProfileOwnerApp) {
	        mDevicePolicyManager.setApplicationRestrictions(admin, packageName, settings);
	    }
	}
1
2
3
4
5
6
��ȡӦ�ó���������Ϣ
private Bundle getApplicationRestrictions(ComponentName admin, String packageName) {
	    Bundle res = null;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.getApplicationRestrictions(admin, packageName);
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
����Ӧ�ó�����𣬹���ĳ����޷������κλ
private String[] setPackagesSuspended(ComponentName admin, String[] packageNames, boolean suspended) {
	    String[] res = null;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.setPackagesSuspended(admin, packageNames, suspended);
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
�Ƿ�Ϊ����Ӧ��
private boolean isPackageSuspended(ComponentName admin, String packageName) {
	    boolean res = false;

	    if (isProfileOwnerApp) {
	        try {
	        	res = mDevicePolicyManager.isPackageSuspended(admin, packageName);
	        } catch (NameNotFoundException e) {
            	Log.w(TAG, "Error getting appName for package: " + packageName, e);
        	}
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
9
10
11
12
ָ���ض�Ӧ�ó���ʼ�մ򿪵�VPN���ӡ��������������������Զ����貢�־û�
private void setAlwaysOnVpnPackage(ComponentName admin, String vpnPackage,
            boolean lockdownEnabled) {
	    if(isProfileOwnerApp) {
	        try {
	        	mDevicePolicyManager.setAlwaysOnVpnPackage(admin, vpnPackage, lockdownEnabled);
	        } catch (NameNotFoundException | UnsupportedOperationException e) {
            	Log.w(TAG, "Error getting appName for package: " + vpnPackage, e);
        	}
	    }
	}
1
2
3
4
5
6
7
8
9
10
��ȡ��VPN���ӵ�Ӧ��
private String getAlwaysOnVpnPackage(ComponentName admin) {
	    String res = null;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.getAlwaysOnVpnPackage(admin);
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
�������һ��Ӧ�ó������ȨAPI�ķ���Ȩ
private void setDelegatedScopes(ComponentName admin, String delegatePackage,
            List<String> scopes) {
	    if(isProfileOwnerApp) {
	        mDevicePolicyManager.setDelegatedScopes(admin, delegatePackage, scopes);
	    }
	}
1
2
3
4
5
6
��ȡ��ȨӦ�õ�����Ȩ��
private List<String> getDelegatedScopes(ComponentName admin, String delegatedPackage) {
	    List<String> res = null;
	    if(isProfileOwnerApp) {
	        res = mDevicePolicyManager.getDelegatedScopes(admin, delegatedPackage);
	    }
	    return res;
	}
1
2
3
4
5
6
7
��װ֤�����Ӧ��˽Կ
private boolean installKeyPair(ComponentName admin, PrivateKey privKey, Certificate cert, String alias) {
	    boolean res = false;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.installKeyPair(admin, privKey, cert, alias);
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
ɾ���ܳ�
private boolean removeKeyPair(ComponentName admin, String alias) {
	    boolean res = false;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.removeKeyPair(admin, alias);
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
��֤���Ƿ�װΪ����CA
private boolean hasCaCertInstalled(ComponentName admin, byte[] certBuffer) {
	    boolean res = false;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.hasCaCertInstalled(admin, certBuffer);
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
ж�������Զ���Ŀ���CA֤�顣��ϵͳCA֤���⣬ͨ���豸��������ķ�ʽ��װ��֤��Ҳ����ɾ��
private void uninstallAllUserCaCerts(ComponentName admin) {
	    if(isProfileOwnerApp) {
	        mDevicePolicyManager.uninstallAllUserCaCerts(admin);
	    }
	}
1
2
3
4
5
���ص�ǰ�����ε�����CA֤�飬������ϵͳCA֤�顣����û�ͨ�����豸����֮���������ʽ��װ���κ�֤�飬��Щ֤��Ҳ���������ڡ�
private List<byte[]> getInstalledCaCerts(ComponentName admin) {
	    List<byte[]> res = null;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.getInstalledCaCerts(admin);
	    }
	    return res;
	}
1
2
3
4
5
6
7
8
�ӿ����û�CAsж�ظ�����֤��
private void uninstallCaCert(ComponentName admin, byte[] certBuffer) {
	    if(isProfileOwnerApp) {
	        mDevicePolicyManager.uninstallCaCert(admin, certBuffer);
	    }
	}
1
2
3
4
5
������֤�鰲װΪ�û�����CA
private boolean installCaCert(ComponentName admin, byte[] certBuffer) {
	    boolean res = false;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.installCaCert(admin, certBuffer);
	    }
	    return res;
	}

���ó�ʱʱ�䣬��ʱ���û�����ʹ�������֤���ܽ���ϵͳ������ָ�ơ������
private void setRequiredStrongAuthTimeout(ComponentName admin, long timeoutMs) {
	    if(isProfileOwnerApp) {
	        mDevicePolicyManager.setRequiredStrongAuthTimeout(admin, timeoutMs);
	    }
	}

��ȡ��ʱʱ��
private long getRequiredStrongAuthTimeout(ComponentName admin) {
	    long res = 0;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.getRequiredStrongAuthTimeout(admin);
	    }
	    return res;
	}

�����豸��������
private boolean setResetPasswordToken(ComponentName admin, byte[] token) {
	    boolean res = false;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.setResetPasswordToken(admin, token);
	    }
	    return res;
	}

��������豸����Token
private boolean clearResetPasswordToken(ComponentName admin) {
	    boolean res = false;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.clearResetPasswordToken(admin);
	    }
	    return res;
	}

�����豸����Token����״̬
private boolean isResetPasswordTokenActive(ComponentName admin) {
	    boolean res = false;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.isResetPasswordTokenActive(admin);
	    }
	    return res;
	}

�����豸�������룬��Token�����״̬����Ч
private boolean resetPasswordWithToken(ComponentName admin, String password,
            byte[] token, int flags) {
	    boolean res = false;

	    if (isProfileOwnerApp) {
	        res = mDevicePolicyManager.resetPasswordWithToken(admin, password, token, flags);
	    }
	    return res;
	}
��������������������������������
ԭ�����ӣ�https://blog.csdn.net/visionliao/article/details/84767383









����DeviceOwner��Ҫע��ļ��㣺
ֻ��Android5.0������Ч��
һ���豸ֻ�ܴ���һ��DeviceOwner��
DeviceOwnerӦ�ò��ܱ�ж�أ�Ҳ�޷�������->��ȫ�йر���Ȩ�ޡ�������취���潲����
��Ϊ�ҵ�Ӣ��ϡ�ã����ºܶ��ĵ��Ͳ����е�ĳЩ��������Ĳ��Ǻ�͸���������ܽ�Ĳ��Ǻܵ�λ����ҽ����ۿ���ʹ�á�

����DeviceOwner3�ַ�ʽ
1. ����NFC�������ֻ���ʼ����ʱ����һ��DeviceOwnerӦ�õ��ֻ��ϡ��ο� ���� ����δ��֤��
2. ����ADB���������֤��
�Ȱ����DeviceOwnerӦ�ð�װ���豸�ϡ�Ȼ��������������ADB���

$adb shell dpm set-device-owner floatingmuseum.devicemanagersample/.MyDeviceAdminReceiver
������ִ�����ʾ

java.lang.IllegalStateException: Trying to set device owner but device is already provisioned.
�ɳ��Ե�����-�˻���ɾ�������˻���Ȼ�����³���ADB���ã����������������óɹ���

Success: Device owner set to package floatingmuseum.devicemanagersample
Active admin set to component {floatingmuseum.devicemanagersample/floatingmuseum.devicemanagersample.MyDeviceAdminReceiver}
3. ����root�豸�Ͻ��С�������֤��
����/data/system/Ŀ¼�´���һ��device_owner.xml�ļ���

��������

<?xml version="1.0" encoding="utf-8" standalone="yes" ?>
<device-owner package="your owner app packagename" />
Ȼ�������豸��һ��Ҫע���������豸֮ǰ��װ�����DeviceOwnerӦ�ã����������޷�������BUG��


-----------------------------------------------------------------------------------------------------------------------------------


����API�Ĳ���ʹ��
1 ����Ӧ�� setApplicationHidden()

�����ص�Ӧ�ÿ���������Ӧ���б����ҵ��������ص�Ӧ�����°�װ����Ȼ�޷���ʾ��δ��������ϵͳӦ�ú��к�Ч����



2 ���ù̶���Ļ setLockTaskPackages()

���������������Ļ���������Ӧ�����棬���糵վ�ĵ���չ�ƣ��ɴ����ĵ��������ȵȡ�ͨ�����ǿ�����ϵͳ����-��ȫ-��Ļ�̶��������ù̶���Ļ������ʹ��ActivityManager��startLockTask()���������Ϸ�ʽ����û�������Ϣ֪ͨ�û������̶���Ļ�����ṩ�˳��̶���Ļ�ķ�����

�������ʹ��startLockTask֮ǰ����setLockTaskPackages�������᲻����ֱ֪ͨ�ӹ̶���Ļ����������home���Ͳ˵�������������ⰴ���Ļ������޷�ͨ���������ؼ��˳��̶���Ļ������ϵͳΪ��os��׿5.0����Ȼ���Գ������ؼ��˳��������޷�ʹ�ó������ؼ�������������ַ����˳��������豸����ʹ��Activity.stopLockTask()��



3 �����û����� addUserRestrictions()

�������õĹ����кܶ࣬���������������ڣ�Ӧ�ð�װж�أ�WIFI�������ã��ָ����������ɾ���û����绰���ŵȵȣ���ǿ��ĵķ�����

�����������������ںͽ�ֹӦ�ð�װж�أ����������á�

��������ο�UserManager�� SUMMARY ��



4 ���ÿ���ʹ�ø������ܵ�Ӧ�� setPermittedAccessibilityServices()

ʹ�ô˷��������в��ڴ˷��������е�Ӧ�ö�����ʹ�ø������ܣ���ϵͳ����-�����������ѡ����Ϊ��ɫ�����Ƕ�ϵͳӦ����Ч��

������null����ȡ�������޶���



5 ���ÿ���ʹ�õ����뷨 setPermittedInputMethods()

�˷���ֻ�Ե��������뷨��Ч��ϵͳ���뷨���ᱻ���ã������õ����뷨��������ʻ�ɫ��ʾ��

������null����ȡ���޶���



6 ���ý�ֹ��Ļ���� setScreenCaptureDisabled()

ʹ�ô˷�������Ļ¼�����ֻ��¼ȡ������������vysor������Ļ�������Ҳֻ�ܿ���������������Ȼ���Կ���״̬���Լ�toast��ʾ��


7 ȫ������ setGlobalSetting()

����ADB���أ��������أ��ֻ����ӵ���ʱ�Ƿ���Կ���USB�洢�豸ģʽ��������ģʽ���صȵȡ�

ADB��������û�����⡣��USB�洢ģʽ��������豸���Ѿ�û���ˣ�������ģʽ��û���⣬�ر�ûЧ����


8 ��ȫ���� setSecureSetting()

����Ĭ�����뷨����ֹ��װδ֪��ԴӦ�ã�����λ�õȵȡ�





------------------------------------------------------------
��6.0�ϵı仯
��Android6.0�汾�Ϲȸ�������������ʱȨ�޵����룬���DevicePolicyManager��API��Ҳ�������������Ȩ������Ĳ������ֱ�Ϊ��һӦ��Ȩ�����ƣ��Լ�ȫ��Ȩ�����ơ�

1. ��һӦ��Ȩ������ setPermissionGrantState()
˵ʵ�����API��֪�����Ҳ��Եķ������ԣ������������ѵ��ض�˳��ʹ�������ǳ��鷳����������ʱ�����˷�����

���Գ���

����������һ����˷�����Ӧ��������ȡָ��Ӧ�õ�ָ��Ȩ�޵�״̬getPermissionGrantState()��Ȼ���°�װһ��APP����ҪдSD��Ȩ�ޡ�

�趨��Ӧ��дSD��Ȩ��Ϊ�Զ��ܾ���

��ȡ״̬��ʾ��ȻΪPERMISSION_GRANT_STATE_DEFAULT������Ӧ�������в鿴Ȩ�ޣ�дSD��Ȩ��Ϊ��ɫ����ѡ�����Ҵ��ھܾ�״̬������Ӧ����ȥ����Ȩ�ޣ���������Ȩ����ʾ��ֱ��ʧ�ܡ�

�������ϲ��������Ǽ������趨��Ӧ��дSD��Ȩ��Ϊ�Զ���ȡ��

��ȡ״̬�Ծ���ʾΪPERMISSION_GRANT_STATE_DEFAULT��Ӧ�����ò鿴Ȩ��Ϊ��ɫ�����Ǵ���Ȩ���Ѹ����״̬������Ӧ����ȥ����Ȩ�ޣ���������ʾʧ�ܡ�

�������ϲ��裬�趨дSD��Ȩ��ΪĬ��

��ȡ״̬ΪPERMISSION_GRANT_STATE_DEFAULT��Ӧ�������пɲ���������Ϊ��һ�����Զ���ȡ��������ʾȨ���Ѹ���״̬��Ӧ���е����룬��֪�п�����Ȩ�ޡ�

��ֻ������һ���������������BUGҲ��ʱ�����֣��������������Ҫʹ��Ȩ�����ƣ��������

2. ȫ�ֶ�̬Ȩ������ setPermissionPolicy()
��ȫ��Ӧ�õ�Ȩ�޽��г�ʼ���ƣ����Ӧ�õ�Ȩ���ڴ�����֮ǰ�ѱ����ù��������Ǿܾ����Ǹ��裬���������ܴ����õ����ƣ���˵����ֻ��δ��ʼ������Ȩ�޽������ơ�

����״̬��PERMISSION_POLICY_PROMPT��PERMISSION_POLICY_AUTO_GRANT��PERMISSION_POLICY_AUTO_DENY�����룬�Զ����裬�Զ��ܾ���

������״̬Ϊ���õģ������������Զ��ܾ���Ӧ�ð�װ�����ж�̬Ȩ��Ĭ�Ͼܾ��޷��޸ģ���ʹ���ȫ������Ϊ�Զ�����������룬Ӧ����Ȼ���ձ���װʱ��Ȩ�����á�

������Ҫע���ĵ�����仰��

This also applies to new permissions declared by app updates. When a permission is denied or granted this way, the effect is equivalent to setting the permission grant state via setPermissionGrantState(ComponentName, String, String, int).

��˵һ�����Ӱɡ�

�����Ұ�װһ��Ӧ��֮ǰ������ȫ������ΪPERMISSION_POLICY_PROMPT,Ȼ��װ��Ӧ�ú�Ϊ����Ȩ��ǰ�޸�ȫ������ΪPERMISSION_POLICY_GRANT,Ȼ��Ӧ������Ȩ�ޣ����Զ����裬�����޷����������޸ģ��������õ�һӦ��Ȩ�޵�Ч����

�ܵ���˵��������Ӧ�ð�װ��Ȩ��δ����ǰ��ȫ��Ȩ�����÷����˸ı䣬���Ϊ�Զ���������Զ��ܾ��Ļ�����������Ȩ�ޣ�Ч����͵�һӦ��Ȩ������һ����ȫ���������Զ��ܾ����������Զ��ܾ��������ñ���޷��޸ģ�ȫ�������Զ����裬�����������Զ����貢�����ñ���޷��޸ġ�

3.����״̬�� setStatusBarDisabled()
���û������Է���ʹ�á�





















-----------------------------------------------------------------------------------------------------

Android�ṩ�������豸��������Device Administration(�豸����Ա), ProfileOwner(�����ļ�������)�� DeviceOwner(�豸������)�������ֹ�������Ӧ���ֵȼ��Ĺ���Ȩ�ޣ���Եģ��ȼ�Խ����ӵ�еĹ���Ȩ��Խ�ߣ����ٵķ���Ҳ�Դ����ԣ�Ҫ��һ��Ӧ�����ó�Ϊ��Щ�����豸��Ҳ��Ҫ��ͬ��Ȩ�޵ȼ���

���� Device Administration
Ҫ����һ��DeviceAdmin ����ҪȨ�������˵����С�ģ�Androidϵͳ�ṩ��һ�ַ�����

Intent intent = new Intent(
	DevicePolicyManager.ACTION_ADD_DEVICE_ADMIN);
intent.putExtra(DevicePolicyManager.EXTRA_DEVICE_ADMIN,
	mComponentName);
intent.putExtra(DevicePolicyManager.EXTRA_ADD_EXPLANATION, "��ʾ����");
startActivityForResult(intent, 1);
1
2
3
4
5
6
�÷���������DeviceAdmin�Ķ���ί�и�ϵͳSettings���н�����ʾ�û��Ƿ񼤻�/ͣ��/ж��һ���豸����Ӧ�á����ַ�����ʵ��һ�ֶ�̬Ȩ�ޣ����û������Ƿ������豸������������ҵ�У���Щ������Ӧ�����û��������ɹ���ƽ̨�ں�̨һ�����á�
���һ��Ӧ�õĽ�������system����ô�ͺ�ϵͳSettings������ͬ��Ȩ�ޣ����ǿ�����ϵͳ�����һ�������ĳ�������һ�������Լ���DeviceAdmin����

/**
 * ����DeviceAdmin
 * packageName: Ӧ�ó������
 * policyReceiver: �̳���DeviceAdminReceiver������
 */
public static void setActiveAdmin(String packageName, String policyReceiver) {
    // 1. ������������ת��ΪComponentName
    ComponentName component = new ComponentName(packageName, policyReceiver);
    // 2. ͨ��ComponentName��ȡActivityInfo�����Ϊ�գ�˵��������������ϵͳ�и������������Ӧ�ã�ֱ�ӷ���
    ActivityInfo ai = null;
    try {
        ai = iPackageManager.getReceiverInfo(component,
                PackageManager.GET_META_DATA |
                PackageManager.GET_DISABLED_UNTIL_USED_COMPONENTS |
                PackageManager.MATCH_DIRECT_BOOT_UNAWARE |
                PackageManager.MATCH_DIRECT_BOOT_AWARE, getMyUserId());
    } catch (RemoteException e) {
        debug("Unable to load component: " + component);
    }
    // 3. ����DevicePolicyManager�����з���setActiveAdmin(ϵͳ��Ӧ����Ȩ��)
    mDevicePolicyManager.setActiveAdmin(component, true /*refreshing*/, mUserId);
}
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
/**
 * ͨ�������ж�һ�������Ƿ�Ϊ�����DeviceAdmin
 * packageName: Ӧ�ó������
 * return
 *      true: ��
 *      false: ����
 */
public static boolean packageHasActiveAdmins(String packageName) {
    // packageHasActiveAdmins�������Ϊ@hide��ֻ��ϵͳӦ�ÿ��Ե���
    DevicePolicyManager devicePolicyManager = (DevicePolicyManager) getSystemService(Context.DEVICE_POLICY_SERVICE);
    return devicePolicyManager.packageHasActiveAdmins(packageName);
}
1
2
3
4
5
6
7
8
9
10
11
12
�˽����DeviceAdmin��Ȩ���Լ�API��ʹ�����飬��ת����������Android Device Administration Ӧ�õ�����

���� ProfileOwner
֮ǰ���ܹ���ProfileOwner �ڹ��ڿ��ܲ�����(Android DevicePolicyManager �豸������������˵��)����������һ��ProfileOwner�����м���;���������뽲�⣬����ֻ����һ������:
����system���̵�ϵͳӦ�ã�������ProfileOwner�����������������ϵͳ��ʵ��һ��ϵͳӦ�ã���¶һ��һ������ProfileOwner�Ľӿڣ�

/**
 * ����ProfileOwner
 * packageName: Ӧ�ó������
 * policyReceiver: �̳���DeviceAdminReceiver����
 * deviceUserName: ΪProfileOwner����һ�����֣��粻���ô�null
 * return
 *      true:  ���óɹ�
 *      false: ����ʧ��
 * (����ƪ������ֻ�����˹ؼ����룬һ�����߼�����������ʡ��)
 */
public static boolean setProfileOwner(String packageName, String policyReceiver, String deviceUserName) {
    // 1. ������������ת��ΪComponentName
    ComponentName component = new ComponentName(packageName, policyReceiver);
    // 2. ͨ��ComponentName��ȡActivityInfo�����Ϊ�գ�˵��������������ϵͳ�и������������Ӧ�ã�ֱ�ӷ���
    ActivityInfo ai = null;
    try {
        ai = iPackageManager.getReceiverInfo(component,
                PackageManager.GET_META_DATA |
                PackageManager.GET_DISABLED_UNTIL_USED_COMPONENTS |
                PackageManager.MATCH_DIRECT_BOOT_UNAWARE |
                PackageManager.MATCH_DIRECT_BOOT_AWARE, getMyUserId());
    } catch (RemoteException e) {
        debug("Unable to load component: " + component);
    }
    // 3. ����DevicePolicyManager�����з���setActiveAdmin(ϵͳ��Ӧ����Ȩ��)
    mDevicePolicyManager.setActiveAdmin(component, true /*refreshing*/, mUserId);
    // 4. ����setProfileOwner
    try {
        result = mDevicePolicyManager.setProfileOwner(component, deviceUserName, mUserId);
        debug("set package " + component + " as profile owner result: " + result);
    } catch (RemoteException | IllegalArgumentException | IllegalStateException e) {
        debug("Error: setProfileOwner failed to " + component.flattenToShortString() + " Error Info: " + e);
        // �������ProfileOwner�쳣�������õ�DeviceAdmin����Ҳһ��ȡ��
        try {
            mDevicePolicyManager.removeActiveAdmin(component, mUserId);
        } catch (RemoteException e2) {
            debug("Error: removeActiveAdmin failed to " + component.toString() + " Error Info: " + e2);
        }
    }
    if (result) {
        try {
            mDevicePolicyManager.setUserProvisioningState(DevicePolicyManager.STATE_USER_SETUP_FINALIZED, mUserId);
        } catch (RemoteException e) {
            debug("Error: setUserProvisioningState failed to " + component.toString() + " Error Info: " + e);
        }
        debug("Success: Active admin and profile owner set to " + component.toShortString() + " for user " + mUserId);
    }
}
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
48
��һ��Ӧ�ó�Ϊ��ProfileOwnerӦ�ã�����ӵ�������е�ProfileOwner���������˽����ProfileOwner��Ȩ���Լ�API��ʹ�����飬��ת����������Android ProfileOwner Ӧ�õ�������

���� DeviceOwner
DeviceOwner����ʹһ��������Ӧ�ó���ӵ��ϵͳ��߹���Ȩ�ޣ����ٵķ���Ҳ�����ġ� Ҫ����һ��DeviceOwner����, ��Ҫ�ܸߵ�Ȩ�ޣ�ϵͳ�ṩ���ַ�ʽ��

adb shell
msm8953_64:/ # 
msm8953_64:/ # dpm set-device-owner --name Test com.action.deviceadmin/.DPMTestReceiver
-----------------------mName Test
mComponent: {com.action.deviceadmin/com.action.deviceadmin.DPMTestReceiver}, mName: Test, mUserId: 0
Success: Device owner set to package ComponentInfo{com.action.deviceadmin/com.action.deviceadmin.DPMTestReceiver}
Active admin set to component {com.action.deviceadmin/com.action.deviceadmin.DPMTestReceiver}
msm8953_64:/ # 
1
2
3
4
5
6
7
ͨ��dpm��������һ��DeviceOwner��
��������������������������������
ԭ�����ӣ�https://blog.csdn.net/visionliao/article/details/84768035


