import React, { useState } from 'react';
import { Star, Zap, Clock, Info, Search, Filter, Map, MapPin, ChevronDown, ChevronUp, AlertCircle, Users, Ticket, UserCheck, Ruler, CreditCard, Box, Sparkles, Construction, Ghost, Monitor } from 'lucide-react';

const App = () => {
  const [searchTerm, setSearchTerm] = useState('');
  const [selectedLocation, setSelectedLocation] = useState('전체');
  const [selectedCategory, setSelectedCategory] = useState('전체');
  const [expandedId, setExpandedId] = useState(null);

  const categories = ['전체', '스릴', '패밀리', '롤러코스터', '키즈', '다크라이드', '체험', '시어터', '슈팅', '모노레일'];
  const locations = ['전체', '어드벤처 4F', '어드벤처 3F', '어드벤처 2F', '어드벤처 1F', '언더랜드(B1)', '키디존', '매직아일랜드', '메이플 아일랜드'];

  const rides = [
    // 4F
    { 
      id: 1, name: "파라오의 분노", location: "어드벤처 4F", type: "멀티모션 다크라이드", category: "다크라이드", 
      fun: 4.5, thrill: 3.5, wait: 5, 
      description: "정교한 이집트 신전 내부를 지프차로 탐험하는 모험.",
      tags: ["가족", "어드벤처"], 
      height: "110cm 이상", weight: null,
      info: { reservation: false, single: false, kidsOnly: false, phobia: false, paid: false, is3D: false, isPopular: true },
      details: "실제 보물을 찾는 듯한 정교한 세트장이 일품입니다. 매일 오후 2시 30분부터 3시 30분까지 점검을 합니다. 싱글라이더가 사라졌습니다."
    },
    { 
      id: 2, name: "풍선비행", location: "어드벤처 4F", type: "공중궤도 라이드(공중 모노레일)", category: "패밀리", 
      fun: 2.5, thrill: 1.5, wait: 4.5, 
      description: "하늘 위에서 롯데월드 전체를 조망하는 낭만적인 비행.",
      tags: ["고소공포주의", "뷰맛집"], 
      height: null, weight: null,
      info: { reservation: false, single: false, kidsOnly: false, phobia: true, paid: false, is3D: false, isPopular: true },
      details: "상당히 높은 곳에서 이동하므로 고소공포증이 있다면 주의하세요."
    },
    { 
      id: 3, name: "어크로스다크", location: "어드벤처 4F", type: "시어터형 라이드", category: "체험", 
      fun: 2.5, thrill: 1, wait: 1.5, 
      description: "우주 공간을 배경으로 펼쳐지는 초대형 시네마틱 시어터 모험.",
      tags: ["시어터", "우주", "영상"], 
      height: "110cm 이상", weight: null,
      info: { reservation: false, single: false, kidsOnly: false, phobia: false, paid: false, is3D: true, isPopular: false },
      details: "광활한 우주 영상을 감상하며 즐기는 몰입형 시어터 시설입니다. 좌석의 움직임은 진동 제외 거의 존재하지 않습니다."
    },
    // 3F
    { 
      id: 4, name: "콩 X 고질라: 더 라이드", location: "어드벤처 3F", type: "다이나믹 라이드", category: "다크라이드", 
      fun: "?", thrill: "?", wait: "?", 
      description: "거대 괴수들의 전쟁 한복판으로 뛰어드는 압도적 스케일의 라이드.",
      tags: ["예정", "괴수", "블록버스터"], 
      height: "준비 중", weight: null,
      info: { isPlanned: true, reservation: false, single: false, kidsOnly: false, phobia: false, paid: false, is3D: true, isPopular: false },
      details: "3층에 새롭게 선보일 예정인 글로벌 IP 콜라보레이션 시설입니다."
    },
    { 
      id: 5, name: "월드모노레일 (어드벤처)", location: "어드벤처 3F", type: "모노레일", category: "패밀리", 
      fun: 3, thrill: 0.5, wait: 3, 
      description: "어드벤처 내부를 한 바퀴 도는 모노레일.",
      tags: ["내부순환", "휴식"], 
      height: "6세 이상(미만 시 보호자 동반)", weight: null,
      info: { reservation: false, single: false, kidsOnly: false, phobia: false, paid: false, is3D: false, isPopular: false },
      details: "현재 매직아일랜드로 나가는 노선은 운영하지 않으며 실내만 순환합니다."
    },
    { 
      id: 6, name: "게임 빌리지", location: "어드벤처 3F", type: "아케이드", category: "체험", 
      fun: 4, thrill: 1, wait: 1, 
      description: "다양한 게임기와 즐길 거리가 가득한 대형 오락실.",
      tags: ["오락실", "자유이용권제외"], 
      height: "제한 없음", weight: null,
      info: { reservation: false, single: false, kidsOnly: false, phobia: false, paid: true, is3D: false, isPopular: false },
      details: "각 게임기마다 별도의 이용 요금이 발생합니다."
    },
    // 2F
    { 
      id: 7, name: "후렌치 레볼루션", location: "어드벤처 2F", type: "롤러코스터", category: "스릴", 
      fun: 4.5, thrill: 4.5, wait: 4.5, 
      description: "360도 회전하며 건물 사이를 아슬아슬하게 통과하는 코스터.",
      tags: ["싱글라이더", "스릴러"], 
      height: "120cm 이상", weight: null,
      info: { reservation: true, single: true, kidsOnly: false, phobia: true, paid: false, is3D: false, isPopular: true },
      details: "실내 최고의 인기 시설입니다."
    },
    { 
      id: 8, name: "범퍼카 (어드벤처)", location: "어드벤처 2F", type: "범퍼카", category: "패밀리", 
      fun: 4, thrill: 2, wait: 3.5, 
      description: "좌충우돌 부딪히며 즐기는 짜릿한 운전 경험.",
      tags: ["운전", "스트레스해소"], 
      height: "140cm 이상", weight: null,
      info: { reservation: false, single: false, kidsOnly: false, phobia: false, paid: false, is3D: false, isPopular: false },
      details: "성인 및 청소년용 범퍼카입니다."
    },
    // 1F
    { 
      id: 9, name: "신밧드의 모험", location: "어드벤처 1F", type: "보트 라이드", category: "다크라이드", 
      fun: 4, thrill: 2, wait: 2.5, 
      description: "지하 동굴 속 신밧드의 모험 이야기를 따라가는 보트 여행.",
      tags: ["스토리", "지하탐험"], 
      height: "110cm 이상", weight: null,
      info: { reservation: false, single: false, kidsOnly: false, phobia: false, paid: false, is3D: false, isPopular: false },
      details: "작은 하강 구간이 두 번 있습니다."
    },
    { 
      id: 10, name: "스페인 해적선", location: "어드벤처 1F", type: "바이킹", category: "스릴", 
      fun: 4, thrill: 4, wait: 3.5, 
      description: "천장에 닿을 듯 올라가는 짜릿한 무중력 상태의 경험.",
      tags: ["무중력", "스릴"], 
      height: "110cm 이상", weight: null,
      info: { reservation: false, single: false, kidsOnly: false, phobia: true, paid: false, is3D: false, isPopular: true },
      details: "뒷자리가 가장 스릴 넘칩니다."
    },
    { 
      id: 11, name: "후룸라이드", location: "어드벤처 1F", type: "워터 라이드", category: "스릴", 
      fun: 4.5, thrill: 3, wait: 4.5, 
      description: "통나무 배를 타고 급류를 헤쳐나가는 시원한 폭포 하강.",
      tags: ["물튐주의", "커플추천"], 
      height: "110cm 이상", weight: null,
      info: { reservation: true, single: false, kidsOnly: false, phobia: false, paid: false, is3D: false, isPopular: true },
      details: "탑승 시 물이 많이 튈 수 있습니다."
    },
    { 
      id: 12, name: "회전바구니", location: "어드벤처 1F", type: "회전 시설", category: "패밀리", 
      fun: 3.5, thrill: 3.5, wait: 2, 
      description: "빙글빙글 돌아가는 바구니 안에서 즐기는 어지러운 즐거움.",
      tags: ["어지럼증주의", "직접회전"], 
      height: "100cm 이상", weight: null,
      info: { reservation: false, single: false, kidsOnly: false, phobia: false, paid: false, is3D: false, isPopular: false },
      details: "핸들을 돌리면 속도가 빨라집니다."
    },
    { 
      id: 13, name: "툼 오브 호러", location: "어드벤처 1F", type: "공포 체험", category: "체험", 
      fun: 3.5, thrill: 3, wait: 2, 
      description: "어둠 속에서 갑자기 나타나는 유령과의 공포 조우.",
      tags: ["공포", "심장주의"], 
      height: "전연령", weight: null,
      info: { reservation: false, single: false, kidsOnly: false, phobia: false, paid: true, is3D: false, isPopular: false },
      details: "유료 시설입니다."
    },
    { 
      id: 14, name: "로티트레인", location: "어드벤처 1F", type: "열차", category: "패밀리", 
      fun: 3, thrill: 0, wait: 2, 
      description: "어드벤처 1층을 유유히 누비는 귀여운 로티 기차.",
      tags: ["기차", "가족", "로티"], 
      height: "전연령", weight: null,
      info: { reservation: false, single: false, kidsOnly: false, phobia: false, paid: false, is3D: false, isPopular: false },
      details: "퍼레이드 준비 시간엔 운행이 중단됩니다."
    },
    { 
      id: 15, name: "배틀그라운드 월드 에이전트", location: "어드벤처 1F", type: "슈팅 라이드", category: "체험", 
      fun: 4.5, thrill: 2, wait: 4, 
      description: "실제 배틀그라운드 세계관 속에서 펼치는 실감나는 슈팅 훈련.",
      tags: ["슈팅", "신규", "배그"], 
      height: "120cm 이상", weight: null,
      info: { reservation: true, single: false, kidsOnly: false, phobia: false, paid: false, is3D: true, isPopular: true },
      details: "최신 인기 시설입니다."
    },
    { 
      id: 16, name: "플라이 벤처", location: "어드벤처 1F", type: "플라잉 시어터", category: "체험", 
      fun: 4.5, thrill: 2.5, wait: 3.5, 
      description: "거대한 스크린 앞에서 하늘을 나는 듯한 기분을 느끼는 체험.",
      tags: ["비행체험", "영상미"], 
      height: "140cm 이상 (120~140cm 보호자 동반)", weight: null,
      info: { reservation: false, single: false, kidsOnly: false, phobia: true, paid: false, is3D: false, isPopular: true },
      details: "영상미가 훌륭합니다."
    },
    { 
      id: 17, name: "회전목마", location: "어드벤처 1F", type: "회전목마", category: "패밀리", 
      fun: 3, thrill: 0.5, wait: 2.5, 
      description: "64마리의 백마와 함께하는 환상적인 사진 명소.",
      tags: ["포토존", "커플", "가족"], 
      height: "100cm 이상", weight: null,
      info: { reservation: false, single: false, kidsOnly: false, phobia: false, paid: false, is3D: false, isPopular: true },
      details: "밤에 더 아름답습니다."
    },
    { 
      id: 18, name: "키즈토리아", location: "어드벤처 1F", type: "어린이 놀이터", category: "키즈", 
      fun: 4, thrill: 0, wait: 3, 
      description: "동화 속 세상을 재현한 거대 소프트 폼 놀이터.",
      tags: ["놀이터", "어린이전용"], 
      height: "120cm 이하", weight: null,
      info: { reservation: true, single: false, kidsOnly: true, phobia: false, paid: false, is3D: false, isPopular: true },
      details: "입장 시간이 정해져 있습니다."
    },
    { 
      id: 19, name: "3D 황야의 무법자 2", location: "어드벤처 1F", type: "슈팅", category: "체험", 
      fun: 3.5, thrill: 1, wait: 2, 
      description: "말을 타고 달리는 실감나는 3D 슈팅 게임.",
      tags: ["슈팅", "서부", "3D"], 
      height: "120cm 이상", weight: null,
      info: { reservation: false, single: false, kidsOnly: false, phobia: false, paid: false, is3D: true, isPopular: false },
      details: "1등에 도전해보세요."
    },
    { 
      id: 20, name: "드래곤 와일드 슈팅", location: "어드벤처 1F", type: "슈팅 라이드", category: "다크라이드", 
      fun: 3.5, thrill: 1, wait: 2, 
      description: "성을 침입한 드래곤들을 향해 레이저 총을 쏘는 모험.",
      tags: ["슈팅", "가족", "드래곤"], 
      height: "110cm 이상", weight: null,
      info: { reservation: false, single: false, kidsOnly: false, phobia: false, paid: false, is3D: false, isPopular: false },
      details: "가족 점수 내기에 좋습니다."
    },
    { 
      id: 21, name: "카트라이더 레이싱 월드", location: "어드벤처 1F", type: "카트 레이싱", category: "체험", 
      fun: 4, thrill: 2, wait: 4, 
      description: "실제 카트를 타고 레이싱 실력을 뽐내는 체험 공간.",
      tags: ["레이싱", "카트라이더"], 
      height: "130cm 이상", weight: null,
      info: { reservation: true, single: false, kidsOnly: false, phobia: false, paid: false, is3D: false, isPopular: true },
      details: "현장 예약 필수입니다."
    },
    { 
      id: 22, name: "벨리곰: 미스터리 멘션", location: "어드벤처 1F", type: "체험형 전시", category: "체험", 
      fun: 3, thrill: 1, wait: 2, 
      description: "벨리곰과 함께하는 미스터리한 공간 체험.",
      tags: ["포토존", "벨리곰"], 
      height: "전연령", weight: null,
      info: { reservation: false, single: false, kidsOnly: false, phobia: false, paid: true, is3D: false, isPopular: false },
      details: "유료 전시입니다."
    },
    // 언더랜드 B1
    { 
      id: 23, name: "와일드 윙/정글/밸리", location: "언더랜드(B1)", type: "4D 라이드", category: "체험", 
      fun: 4, thrill: 2.5, wait: 3, 
      description: "지프, 비행기, 보트를 타고 정글과 하늘, 계곡을 질주하는 4D 모험.",
      tags: ["4D", "모험", "언더랜드"], 
      height: "110cm 이상", weight: null,
      info: { reservation: false, single: false, kidsOnly: false, phobia: false, paid: false, is3D: true, isPopular: false },
      details: "언더랜드의 대표 라이드입니다."
    },
    { 
      id: 24, name: "4D 슈팅어드벤처", location: "언더랜드(B1)", type: "슈팅 라이드", category: "체험", 
      fun: 3.5, thrill: 1.5, wait: 2, 
      description: "화면 속 적들을 향해 총을 쏘는 실감나는 슈팅 게임.",
      tags: ["슈팅", "4D"], 
      height: "110cm 이상", weight: null,
      info: { reservation: false, single: false, kidsOnly: false, phobia: false, paid: false, is3D: true, isPopular: false },
      details: "순위가 발표됩니다."
    },
    // 키디존
    { 
      id: 25, name: "언더씨킹덤", location: "키디존", type: "어린이 놀이터", category: "키즈", 
      fun: 4, thrill: 0.5, wait: 2, 
      description: "바닷속 세상을 꾸며놓은 어린이 전용 실내 놀이 공간.",
      tags: ["놀이터", "어린이전용"], 
      height: "105cm ~ 120cm 권장", weight: null,
      info: { reservation: false, single: false, kidsOnly: true, phobia: false, paid: false, is3D: false, isPopular: false },
      details: "부모님 동반이 가능합니다."
    },
    { 
      id: 26, name: "유레카", location: "키디존", type: "어린이 회전기구", category: "키즈", 
      fun: 3, thrill: 1, wait: 1.5, 
      description: "위아래로 움직이며 하늘을 나는 발명가들의 탈것.",
      tags: ["회전", "어린이"], 
      height: "110cm ~ 140cm (미만 보호자 동반)", weight: null,
      info: { reservation: false, single: false, kidsOnly: true, phobia: false, paid: false, is3D: false, isPopular: false },
      details: "열심히 페달을 밟아보세요."
    },
    { 
      id: 27, name: "점핑피쉬", location: "키디존", type: "회전 시설", category: "키즈", 
      fun: 4, thrill: 3, wait: 2.5, 
      description: "물고기를 타고 코너를 돌 때마다 튕겨나가는 재미.",
      tags: ["스릴키즈", "물고기"], 
      height: "110cm 이상 (미만 보호자 동반)", weight: null,
      info: { reservation: false, single: false, kidsOnly: true, phobia: false, paid: false, is3D: false, isPopular: true },
      details: "속도감이 꽤 있습니다."
    },
    { 
      id: 28, name: "햇님달님", location: "키디존", type: "어린이 드롭", category: "키즈", 
      fun: 3.5, thrill: 2.5, wait: 2, 
      description: "올라갔다 내려오는 어린이용 미니 자이로드롭.",
      tags: ["미니드롭", "인기키즈"], 
      height: "90cm ~ 140cm", weight: null,
      info: { reservation: false, single: false, kidsOnly: true, phobia: false, paid: false, is3D: false, isPopular: false },
      details: "어린이들의 최고 인기 시설입니다."
    },
    { 
      id: 29, name: "어린이 범퍼카", location: "키디존", type: "어린이 범퍼카", category: "키즈", 
      fun: 3.5, thrill: 1.5, wait: 3, 
      description: "어린이들만 운전하며 부딪히는 안전한 범퍼카.",
      tags: ["범퍼카", "어린이"], 
      height: "110cm ~ 140cm", weight: null,
      info: { reservation: false, single: false, kidsOnly: true, phobia: false, paid: false, is3D: false, isPopular: false },
      details: "어른은 탈 수 없습니다."
    },
    { 
      id: 30, name: "스윙팡팡", location: "키디존", type: "회전 기구", category: "키즈", 
      fun: 3, thrill: 1, wait: 2, 
      description: "빙글빙글 돌며 위아래로 팡팡 튀는 재미.",
      tags: ["회전", "어린이"], 
      height: "110cm 미만 보호자 동반", weight: null,
      info: { reservation: false, single: false, kidsOnly: true, phobia: false, paid: false, is3D: false, isPopular: false },
      details: "바구니 테마입니다."
    },
    { 
      id: 31, name: "매직붕붕카", location: "키디존", type: "어린이 열차", category: "키즈", 
      fun: 3, thrill: 0.5, wait: 2, 
      description: "과자나라로 떠나는 귀여운 자동차 여행.",
      tags: ["자동차", "동화"], 
      height: "110cm 미만 보호자 동반", weight: null,
      info: { reservation: false, single: false, kidsOnly: true, phobia: false, paid: false, is3D: false, isPopular: false },
      details: "안전한 주행 기구입니다."
    },
    { 
      id: 32, name: "어린이 동화극장", location: "키디존", type: "공연장", category: "키즈", 
      fun: 4, thrill: 0, wait: 1, 
      description: "로티, 로리와 친구들이 들려주는 동화 이야기.",
      tags: ["공연", "인형극"], 
      height: "전연령", weight: null,
      info: { reservation: false, single: false, kidsOnly: true, phobia: false, paid: false, is3D: false, isPopular: false },
      details: "공연 시간을 확인하세요."
    },
    // 매직아일랜드
    { 
      id: 35, name: "아트란티스", location: "매직아일랜드", type: "급발진 코스터", category: "스릴", 
      fun: 5, thrill: 5, wait: 5, 
      description: "시속 72km 급발진과 롤러코스터의 짜릿함을 동시에.",
      tags: ["예약제", "강력스릴", "대표기구"], 
      height: "135cm ~ 190cm", weight: "100kg 미만",
      info: { reservation: true, single: false, kidsOnly: false, phobia: true, paid: false, is3D: false, isPopular: true },
      details: "롯데월드 1위 인기 기구입니다."
    },
    { 
      id: 36, name: "자이로스윙", location: "매직아일랜드", type: "회전 진동", category: "스릴", 
      fun: 4, thrill: 4.5, wait: 4, 
      description: "거대한 원판이 회전하며 공중으로 솟구치는 스윙.",
      tags: ["강력스릴", "회전스윙"], 
      height: "130cm ~ 190cm", weight: null,
      info: { reservation: false, single: false, kidsOnly: false, phobia: true, paid: false, is3D: false, isPopular: true },
      details: "석촌호수 풍경이 압권입니다."
    },
    { 
      id: 37, name: "월드모노레일 (매직)", location: "매직아일랜드", type: "모노레일", category: "패밀리", 
      fun: 3, thrill: 0.5, wait: 3, 
      description: "매직아일랜드의 아름다운 전경을 감상하는 모노레일.",
      tags: ["호수뷰", "뷰맛집"], 
      height: "6세 이상(미만 보호자 동반)", weight: null,
      info: { reservation: false, single: false, kidsOnly: false, phobia: false, paid: false, is3D: false, isPopular: false },
      details: "야경 감상에 최고입니다."
    },
    { 
      id: 38, name: "쁘띠빵빵", location: "매직아일랜드", type: "자동차", category: "키즈", 
      fun: 3, thrill: 1, wait: 2, 
      description: "호수 주변을 따라 달리는 귀여운 꼬마 자동차.",
      tags: ["자동차", "호수뷰"], 
      height: "110cm 미만 보호자 동반", weight: null,
      info: { reservation: false, single: false, kidsOnly: true, phobia: false, paid: false, is3D: false, isPopular: false },
      details: "가족용입니다."
    },
    { 
      id: 39, name: "자이로드롭", location: "매직아일랜드", type: "자유낙하", category: "스릴", 
      fun: 3.5, thrill: 5, wait: 3, 
      description: "70m 상공에서 단 2초 만에 지상으로 떨어지는 공포.",
      tags: ["고소공포주의", "전망"], 
      height: "130cm ~ 190cm", weight: null,
      info: { reservation: false, single: false, kidsOnly: false, phobia: true, paid: false, is3D: false, isPopular: true },
      details: "무서운 만큼 짜릿합니다."
    },
    { 
      id: 40, name: "환타지 드림", location: "매직아일랜드", type: "다크라이드", category: "패밀리", 
      fun: 3, thrill: 0.5, wait: 2, 
      description: "지하 세계의 요정들을 만나는 꿈같은 기차 여행.",
      tags: ["동화", "가족"], 
      height: "110cm 미만 보호자 동반", weight: null,
      info: { reservation: false, single: false, kidsOnly: false, phobia: false, paid: false, is3D: false, isPopular: false },
      details: "상당히 깁니다."
    },
    { 
      id: 41, name: "문보트", location: "매직아일랜드", type: "보트", category: "체험", 
      fun: 4, thrill: 1, wait: 4, 
      description: "석촌호수 위에서 즐기는 로맨틱한 달 보트.",
      tags: ["야간추천", "로맨틱"], 
      height: "전연령", weight: null,
      info: { reservation: false, single: false, kidsOnly: false, phobia: false, paid: true, is3D: false, isPopular: false },
      details: "별도 요금이 발생합니다."
    },
    { 
      id: 42, name: "혜성특급", location: "매직아일랜드", type: "회전 코스터", category: "롤러코스터", 
      fun: 4.5, thrill: 3.5, wait: 4.5, 
      description: "어두운 우주 공간을 회전하며 질주하는 환상적인 코스터.",
      tags: ["인기기구", "우주", "물품보관함"], 
      height: "120cm 이상", weight: null,
      info: { reservation: true, single: false, kidsOnly: false, phobia: false, paid: false, is3D: false, isPopular: true },
      details: "의자가 뱅글뱅글 돕니다."
    },
    { 
      id: 43, name: "자이로스핀", location: "매직아일랜드", type: "입체 회전", category: "스릴", 
      fun: 3.5, thrill: 3, wait: 3, 
      description: "입체적으로 회전하며 좌우로 움직이는 짜릿한 스핀.",
      tags: ["회전", "석촌호수"], 
      height: "130cm 이상", weight: null,
      info: { reservation: false, single: false, kidsOnly: false, phobia: false, paid: false, is3D: false, isPopular: false },
      details: "풍경이 시원합니다."
    },
    // 메이플 아일랜드 (예정)
    { 
      id: 100, name: "스톤 익스프레스", location: "메이플 아일랜드", type: "패밀리 코스터", category: "패밀리", 
      fun: "?", thrill: "?", wait: "?", 
      description: "메이플스토리 세계관을 배경으로 온 가족이 즐기는 패밀리 코스터.",
      tags: ["오픈예정", "메이플스토리", "가족형"], 
      height: "준비 중", weight: null,
      info: { isPlanned: true, reservation: false, single: false, kidsOnly: false, phobia: false, paid: false, is3D: false, isPopular: false },
      details: "가족 타겟의 경쾌한 주행을 기대할 수 있습니다. 스릴은 낮을 걸로 보입니다."
    },
    { 
      id: 101, name: "에오스 타워", location: "메이플 아일랜드", type: "타워 라이드", category: "스릴", 
      fun: "?", thrill: "?", wait: "?", 
      description: "번지드롭과 햇님달님의 재미를 동시에 느끼는 타워형 수직 낙하 기구.",
      tags: ["오픈예정", "타워", "드롭"], 
      height: "준비 중", weight: null,
      info: { isPlanned: true, reservation: false, single: false, kidsOnly: false, phobia: true, paid: false, is3D: false, isPopular: false },
      details: "에오스 탑을 모티브로 한 넘치는 드롭 시설입니다. 스릴은 낮을 걸로 보입니다."
    },
    { 
      id: 102, name: "아르카나 라이드", location: "메이플 아일랜드", type: "보트 라이드", category: "스피드웨이(회전 보트)", 
      fun: "?", thrill: "?", wait: "?", 
      description: "신비로운 정령의 숲 아르카나를 보트를 타고 도는 보트 라이드.",
      tags: ["오픈예정", "아르카나", "탐험"], 
      height: "준비 중", weight: null,
      info: { isPlanned: true, reservation: false, single: false, kidsOnly: false, phobia: false, paid: false, is3D: false, isPopular: false },
      details: "보트를 타고 계속 좌우로 회전하는 보트 라이드입니다. 스릴은 낮을 걸로 보입니다."
    }
  ];

  const filteredRides = rides.filter(ride => {
    const matchesSearch = ride.name.toLowerCase().includes(searchTerm.toLowerCase());
    const matchesLocation = selectedLocation === '전체' || ride.location.includes(selectedLocation);
    const matchesCategory = selectedCategory === '전체' || ride.category === selectedCategory;
    return matchesSearch && matchesLocation && matchesCategory;
  });

  const StatBar = ({ icon: Icon, label, value, color }) => (
    <div className="flex flex-col gap-1 flex-1">
      <div className="flex items-center gap-1 text-[10px] font-bold text-gray-400 uppercase">
        <Icon size={12} className={color} />
        {label}
      </div>
      <div className="h-1.5 w-full bg-gray-100 rounded-full overflow-hidden">
        {value === "?" ? (
          <div className="h-full bg-slate-200 w-full animate-pulse" />
        ) : (
          <div className={`h-full ${color.replace('text-', 'bg-')}`} style={{ width: `${(value / 5) * 100}%` }} />
        )}
      </div>
      <span className="text-[10px] font-bold text-gray-600 mt-0.5">{value} / 5</span>
    </div>
  );

  return (
    <div className="min-h-screen bg-slate-50 text-slate-900 font-sans pb-10">
      {/* Header */}
      <div className="bg-white border-b border-slate-200 sticky top-0 z-20 shadow-sm">
        <div className="max-w-md mx-auto p-4 md:p-6">
          <div className="flex items-center gap-2 mb-4">
            <div className="w-8 h-8 bg-red-500 rounded-lg flex items-center justify-center text-white font-black shadow-lg shadow-red-200">L</div>
            <h1 className="text-xl font-black text-slate-800 tracking-tight">LOTTE WORLD INSIGHT</h1>
          </div>
          
          <div className="relative mb-4">
            <Search className="absolute left-3 top-1/2 -translate-y-1/2 text-slate-400" size={18} />
            <input 
              type="text" 
              placeholder="기구 이름 검색..." 
              className="w-full pl-10 pr-4 py-3 rounded-xl bg-slate-100 border-none text-sm focus:ring-2 focus:ring-red-400 outline-none transition-all"
              value={searchTerm}
              onChange={(e) => setSearchTerm(e.target.value)}
            />
          </div>

          <div className="flex gap-2 overflow-x-auto pb-1 no-scrollbar">
            {categories.map((cat) => (
              <button
                key={cat}
                onClick={() => setSelectedCategory(cat)}
                className={`px-4 py-1.5 rounded-full whitespace-nowrap text-xs font-bold border transition-all ${
                  selectedCategory === cat ? 'bg-red-500 text-white border-red-500 shadow-md' : 'bg-white text-slate-500 border-slate-200'
                }`}
              >
                {cat}
              </button>
            ))}
          </div>
        </div>
      </div>

      <div className="max-w-md mx-auto p-4 space-y-4">
        <div className="flex justify-between items-center px-1">
          <span className="text-xs font-bold text-slate-400 uppercase tracking-wider">{filteredRides.length} Results</span>
          <div className="flex items-center gap-1 text-xs font-bold text-red-500 bg-red-50 px-3 py-1.5 rounded-lg border border-red-100">
            <MapPin size={14} />
            <select className="bg-transparent outline-none cursor-pointer" value={selectedLocation} onChange={(e) => setSelectedLocation(e.target.value)}>
              {locations.map(loc => <option key={loc} value={loc}>{loc}</option>)}
            </select>
          </div>
        </div>

        <div className="grid gap-4">
          {filteredRides.map((ride) => {
            const isExpanded = expandedId === ride.id;
            
            let cardStyle = "bg-white border-slate-100";
            if (ride.info.kidsOnly) cardStyle = "bg-blue-50/50 border-blue-300 shadow-blue-50";
            if (ride.info.paid) cardStyle = "bg-emerald-50/50 border-emerald-300"; 
            if (ride.info.is3D) cardStyle = "bg-orange-50/50 border-orange-400 ring-1 ring-orange-200 shadow-orange-50";
            if (ride.info.isPlanned) cardStyle = "bg-slate-100 border-slate-300 opacity-80";
            if (isExpanded) cardStyle += " ring-2 ring-red-100 border-red-500";

            return (
              <div 
                key={ride.id} 
                className={`rounded-2xl overflow-hidden shadow-sm border transition-all cursor-pointer ${cardStyle} hover:shadow-md`}
                onClick={() => setExpandedId(isExpanded ? null : ride.id)}
              >
                <div className="p-4">
                  <div className="flex justify-between items-start">
                    <div className="flex-1">
                      <div className="flex flex-wrap items-center gap-2 mb-1">
                        <span className="text-[10px] font-bold px-2 py-0.5 rounded bg-white/80 text-slate-500 border border-slate-200 uppercase">{ride.location}</span>
                        {ride.info.kidsOnly && <span className="text-[10px] font-black px-2 py-0.5 rounded bg-blue-500 text-white flex items-center gap-1"><Users size={10}/> 어린이</span>}
                        {ride.info.paid && <span className="text-[10px] font-black px-2 py-0.5 rounded bg-emerald-600 text-white flex items-center gap-1"><CreditCard size={10}/> 유료</span>}
                        {ride.info.is3D && <span className="text-[10px] font-black px-2 py-0.5 rounded bg-orange-600 text-white flex items-center gap-1"><Monitor size={10}/> 3D/시어터</span>}
                        {ride.info.isPlanned && <span className="text-[10px] font-black px-2 py-0.5 rounded bg-slate-500 text-white flex items-center gap-1"><Construction size={10}/> 예정</span>}
                      </div>
                      <div className="flex items-center gap-2">
                        <h3 className="text-lg font-black text-slate-800 tracking-tight">{ride.name}</h3>
                        {ride.info.isPopular && <span className="text-red-500">🔥</span>}
                      </div>
                    </div>
                    <div className="p-1 rounded-full bg-slate-100/50 text-slate-400">
                      {isExpanded ? <ChevronUp size={18} /> : <ChevronDown size={18} />}
                    </div>
                  </div>

                  <p className={`text-xs text-slate-500 mt-2 mb-4 leading-relaxed ${!isExpanded && 'line-clamp-1'}`}>
                    {ride.description}
                  </p>

                  <div className="flex gap-4 p-3 bg-white/60 rounded-xl mb-2 backdrop-blur-sm">
                    <StatBar icon={Star} label="FUN" value={ride.fun} color="text-yellow-500" />
                    <StatBar icon={Zap} label="THRILL" value={ride.thrill} color="text-purple-500" />
                    <StatBar icon={Clock} label="WAIT" value={ride.wait} color="text-red-500" />
                  </div>

                  {isExpanded && (
                    <div className="mt-4 pt-4 border-t border-slate-200/50 space-y-4 animate-in fade-in slide-in-from-top-2 duration-300">
                      <div className="flex flex-wrap gap-1.5">
                        {ride.tags?.map(tag => (
                          <span key={tag} className="text-[10px] font-bold text-slate-500 bg-slate-200/50 px-2 py-1 rounded">#{tag}</span>
                        ))}
                      </div>

                      <div className="grid grid-cols-2 gap-2">
                        <div className="flex items-center gap-2 p-2 rounded-lg bg-white border border-slate-100 shadow-inner">
                          <Ruler size={14} className="text-slate-400" />
                          <span className="text-[11px] font-bold text-slate-600">{ride.height || "제한 없음"}</span>
                        </div>
                        <div className="flex items-center gap-2 p-2 rounded-lg bg-white border border-slate-100 shadow-inner">
                          <AlertCircle size={14} className="text-slate-400" />
                          <span className="text-[11px] font-bold text-slate-600">{ride.weight || "상관 없음"}</span>
                        </div>
                      </div>

                      <div className="flex flex-wrap gap-2">
                        {ride.info.reservation && <div className="flex items-center gap-1.5 px-2.5 py-1 rounded-full bg-indigo-50 text-indigo-700 text-[10px] font-black border border-indigo-100"><Ticket size={12}/> 탑승예약제</div>}
                        {ride.info.single && <div className="flex items-center gap-1.5 px-2.5 py-1 rounded-full bg-emerald-50 text-emerald-700 text-[10px] font-black border border-emerald-100"><UserCheck size={12}/> 싱글라이더</div>}
                        {ride.info.phobia && <div className="flex items-center gap-1.5 px-2.5 py-1 rounded-full bg-orange-50 text-orange-700 text-[10px] font-black border border-orange-100"><AlertCircle size={12}/> 고소공포주의</div>}
                      </div>

                      <div className="p-3 bg-slate-50 rounded-xl border border-slate-200">
                        <p className="text-[11px] font-bold text-slate-600 leading-relaxed">
                          💡 <span className="underline">Tip & Notice</span>: {ride.details}
                        </p>
                      </div>
                    </div>
                  )}
                </div>
              </div>
            );
          })}
        </div>
      </div>

      <div className="max-w-md mx-auto px-4 mt-6">
        <div className="p-4 rounded-2xl bg-slate-900 text-white shadow-xl">
          <div className="flex items-start gap-3 mb-4">
            <div className="p-2 bg-white/10 rounded-lg">
              <Info size={18} className="text-red-400" />
            </div>
            <div className="flex-1">
              <p className="text-xs font-bold text-white/60 mb-2 uppercase tracking-widest">Guide Information</p>
              <p className="text-[10px] leading-tight text-slate-300">
                <span className="text-blue-400 font-bold">키즈 시설</span>은 어린이 기준으로 수치가 작성되었으며, <span className="text-emerald-400 font-bold">유료 시설</span>은 별도의 이용권이 필요합니다.
              </p>
            </div>
          </div>
          <div className="grid grid-cols-2 gap-y-2 border-t border-white/10 pt-4">
            <div className="flex items-center gap-2 text-[10px]"><div className="w-2.5 h-2.5 rounded-full bg-blue-500"></div> 어린이 전용</div>
            <div className="flex items-center gap-2 text-[10px]"><div className="w-2.5 h-2.5 rounded-full bg-emerald-600 border border-emerald-300"></div> 유료 시설</div>
            <div className="flex items-center gap-2 text-[10px]"><div className="w-2.5 h-2.5 rounded-full bg-orange-600 ring-1 ring-orange-300"></div> 3D/시어터</div>
            <div className="flex items-center gap-2 text-[10px]"><span className="text-red-500">🔥</span> 인기 어트랙션</div>
          </div>
        </div>
      </div>
    </div>
  );
};

export default App;
