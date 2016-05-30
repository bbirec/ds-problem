ds-problem
----------
아무리 간단한 시스템이라도 분산 시스템으로 구성하려고 하면 문제가 어려워 진다. 일하면서 겪는 몇가지 문제를 기록해두고, 여러가지 Solution 중에 가장 좋은 방법을 찾으려고 한다.

## Broadcast
몇억의 유저가 있는 글로벌 서비스인데, 등록된 회원 전체에게 최대한 빠르게 전체 이메일을 보내려고 한다. 

 - 이메일을 보내는 기능은 외부 서비스를 사용해서 약 1초 정도의 시간이 걸린다고 가정한다.
 - 가끔 이메일 발송 서비스는 실패할 수 도 있어서 실패하는 경우, Exponential backoff에 따라 총 10번의 시도를 하고 그래도 실패하는 경우 아예 발송하지 않는다. 
 - 전체 유저에 해당하는 이메일 리스트는 하나의 DB에 있으며, 발송중에 가입한 유저에게는 이메일을 보내지 않아도 된다.

## Stream Capture
온라인 동영상 스트리밍을 저장해두려고 한다. 

 - 현재 방송중인 스트림의 주소를 가져오는 API가 존재하는데, Polling으로 1초에 한번씩 불러서 새로 시작한 방송의 녹화를 시작해야 한다.
 - 방송이 시작될때마다 Unique한 id가 부여된다.
 - 한번 방송이 시작되면 언제 끝날지 모르는데 동영상 파일의 크기가 PC의 하드디스크 용량보다 커질 수 있다. 
 - 스트림을 저장하는 PC의 인터넷 상황이 불안정 해서 중간에 끊길 수 있는데, 최대한 빠르게 재시도 해서 저장해야 하며 동영상이 분할되어 저장되어도 상관없다.



