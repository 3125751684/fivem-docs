---
title: �ű�����
weight: 930
description: >
 ������fxOM�ű�����ʱ��֧�֡�
---

CitizenFX֧�ֿɲ���ű�����ʱ�� ��Щ����ʱ��ʵ��ΪCitizenFX���������/���/����ʵ������fxScripting.idl�ж����fxOM��CitizenFX����ģ�ͣ��ӿڡ�

��׫д����ʱ��ʹ�õ��ض��Ľӿڸ�ʽ�ǣ�

|           �ӿ�             |                                        Ŀ��                                      |
| -------------------------- | -------------------------------------------------------------------------------- |
| IScriptRuntime             | Base interface for script runtimes. Exposes basic lifetime management functions. |
| IScriptTickRuntime         | Allows exposing a Tick function for runtimes that need to run periodically.      |
| IScriptEventRuntime        | Allows exposing a TriggerEvent function to handle incoming script events.        |
| IScriptRefRuntime          | Allows exposing function references that can be called, duplicated and cloned.   |
| IScriptFileHandlingRuntime | Allows to mark a script runtime as handling specific files.                      |

���⣬����һ�������ӿڣ��� IScriptHost�������������ݸ��� IScriptRuntime :: Create����

## Interface reference

### IScriptRuntime

#### Create

```cs
void Create(in IScriptHost scriptHost);
```

�����ű�����ʱʱ�����������ô˷����� ͨ���Ľű������ᱣ�档

#### Destroy

```cs
void Destroy();
```

���ű�����ʱ��������ʱ�����������ô˷�����

#### GetParentObject

```cs
void* GetParentObject(); // direct return value, not result_t
```

��Ӧ�÷�����SetParentObject���õĶ���

#### SetParentObject

```cs
void SetParentObject(void* object); // direct return value, not result_t
```

�⽫���ø����� ��ͨ���Ǳ�����`fx :: Resource *`��������C ++��ʵ�ֵ�����ʱ�йء�

#### GetInstanceId

```cs
int GetInstanceId(); // direct return value, not result_t
```

�⽫��������ʱ�ڳ�ʼ��ʱ���������ʵ��ID��

### IScriptTickRuntime

#### Tick

```cs
void Tick();
```

����ÿ��һ֡����һ�Ρ�

### IScriptEventRuntime

#### TriggerEvent

```cs
void TriggerEvent(in char* eventName, in char* argsSerialized, in uint32_t serializedSize, in char* sourceId);
```

ÿ�������¼�ʱ�������ͻ����TriggerEvent�� �� eventName��������ִ���¼������ƣ�
argsSerialized��serializedSize��ʾ�������飨ʹ��ͨ�����л�Լ���������л�����μ������桱���֣����Լ�
sourceId����һ���ַ��������ڱ�ʶ�¼�����Դ��

### IScriptRefRuntime

��ref����һ���������ã���������������Դ�����������ڽű�����ʱ�е���ί��/�رա�
ÿ����������Դ��������һ��������ʶ����������ʹ����Դ���ƣ�ʵ��ID������������������޶���
���ò�Ӧ�������������ü�����ÿ��������Ӧ�뵥��ɾ����ԡ�

#### CallRef

```cs
void CallRef(in int32_t refIdx, in char* argsSerialized, in uint32_t argsSize, out char* retvalSerialized, out uint32_t retvalSize);
```

��������ʱ������������CallRef�� refIdx����Ҫ���õ�ref��argsSerialized / argsSize�����������飬retvalSerialized��retvalSize�����ʱӦ��������ֵ���顣

#### DuplicateRef

```cs
void DuplicateRef(in int32_t refIdx, out int32_t newRefIdx);
```

DuplicateRefӦ�÷���һ���µ����������������ý���refIdx��ͬ���ڲ������������õ�newRefIdx�С�

#### RemoveRef

```cs
void RemoveRef(in int32_t refIdx);
```

RemoveRefӦ��ɾ����refIdx��ʶ�����á�

### IScriptFileHandlingRuntime

#### HandlesFile

```cs
int32_t HandlesFile(in char* scriptFile);
```

Ӧ�÷��ش�����ʱ�Ƿ�Ӧ����ָ�����ļ���

#### LoadFile

```cs
void LoadFile(in char* scriptFile);
```

�˺���Ӧ������ʱ�����ļ���

### IScriptHost

#### InvokeNative

```cs
void InvokeNative(inout NativeCtx context);
```

���ñ��������� �� nativeIdentifier��Ӧ��������������ʶ������ numArguments��Ӧ���������������� arguments��Ӧ������RAGE����ABI֮����ض����ܲ�����

���ڷ����κν���ı������κν�������������ĵĵ�һ�������ֶ��з��ء�

#### OpenSystemFile

��������ϵͳVFS��ָ���ļ���������

#### OpenHostFile

�������������·����`resources��/ resourceName /`������ָ���ļ���������

#### CanonicalizeRef

#### ScriptTrace

### IScriptHostWithResourceData

�����ʹ��IScriptHost�ϵ�QueryInterface��á�

#### GetResourceName

���ظ���Դ�����ơ�

#### GetNumResourceMetaData

��Ӧʹ�ô˹��ܣ���Ӧʹ�ñ����е� {{<native_link "GET_NUM_RESOURCE_METADATA">}} .

#### GetResourceMetaData

��Ӧʹ�ô˹��ܣ���Ӧʹ�ñ����е�  {{<native_link "GET_RESOURCE_METADATA">}} .

### IScriptHostWithManifest

�����ʹ��IScriptHost�ϵ�QueryInterface��á�

#### IsManifestVersionBetween

```cs
bool IsManifestVersionBetween(guid_t* lowerBound, guid_t* upperBound);
```

����������Դ���嵥�汾�Ƿ���GUID���ض���Χ�� (`lowerBound <= guid < upperBound`).

�������һ��GUIDΪ��GUID��������԰汾�Ƿ����/С����һ��GUID��

## Conventions

### Serialization

���л�ʹ��MessagePack���У���Ϊί��/��������ʹ���ض�����չID��
