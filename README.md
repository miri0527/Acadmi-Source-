# 행정의 계정 생성 
 //회원 관리
	
		//아이디
		//username이 string이기 때문에 string으로 변환시켜주기
		
		public List<CollegeVO> getCollege() throws Exception {
			return administratorDAO.getCollege();
		}
		
		public List<DepartmentVO> getDepartment() throws Exception {
			return administratorDAO.getDepartment();
		}
		
		//계정 생성
		public int setStudentAdd(StudentVO studentVO, MemberVO memberVO, MemberSeqVO memberSeqVO) throws Exception {
			memberVO.setPassword(passwordEncoder.encode(memberVO.getPassword()));
			
			int result;
			String year;
			 if(administratorDAO.getYearSeq(memberSeqVO) == null) {
				 result =  administratorDAO.setInsertSeq(memberSeqVO);
				 year=  administratorDAO.getYearSeq(memberSeqVO).toString();
				 Long memberSeq = administratorDAO.getMemberSeq(memberSeqVO);
				 String username;
				 
				 if(memberSeq < 10) {
					  username = year + "000" + memberSeq;
				  }else if(memberSeq < 100) {
					  username = year + "00" + memberSeq;
				  }else if(memberSeq < 1000) {
					  username = year + "0" + memberSeq;
				  }else {
					  username = year + memberSeq;
				  }
				  
				memberVO.setUsername(username);
				
				result = administratorDAO.setMemberAdd(memberVO);
				
				studentVO.setUsername(memberVO.getUsername());
			
				result = administratorDAO.setStudentAdd(studentVO);
				
				Map<String, Object> map = new HashMap<>();
				map.put("username", memberVO.getUsername());
				
				if(memberVO.getCategory() == 0) {
					map.put("roleNum", 2);
				}else if(memberVO.getCategory() == 1) {
					map.put("roleNum", 2);
				}else if(memberVO.getCategory() == 2) {
					map.put("roleNum", 3);
				}else {
					map.put("roleNum", 0);
				}
				
				
				result = administratorDAO.setRoleAdd(map);
				
				return result;
				 
				 
			 }else {
				  year = administratorDAO.getYearSeq(memberSeqVO).toString(); 
				  result = administratorDAO.setUpdateSeq(memberSeqVO);
				  Long memberSeq = administratorDAO.getMemberSeq(memberSeqVO);
				  String username;
				  
				  
				  
				  if(memberSeq < 10) {
					  username = year + "000" + memberSeq;
				  }else if(memberSeq < 100) {
					  username = year + "00" + memberSeq;
				  }else if(memberSeq < 1000) {
					  username = year + "0" + memberSeq;
				  }else {
					  username = year + memberSeq;
				  }
				  
				  
				  memberVO.setUsername(username);
				 
				
				result = administratorDAO.setMemberAdd(memberVO);
				
				studentVO.setUsername(memberVO.getUsername());
				
				result = administratorDAO.setStudentAdd(studentVO);
				
				Map<String, Object> map = new HashMap<>();
				map.put("username", memberVO.getUsername());
				
				if(memberVO.getCategory() == 0) {
					map.put("roleNum", 1);
				}else if(memberVO.getCategory() == 1) {
					map.put("roleNum", 2);
				}else if(memberVO.getCategory() == 2) {
					map.put("roleNum",3);
				}else {
					map.put("roleNum", 0);
				}
				
				
				result = administratorDAO.setRoleAdd(map);
				
				return result;
			 }
		
			
		}