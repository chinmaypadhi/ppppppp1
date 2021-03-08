ALTER procedure [dbo].[SP_CatagoryWise_Admission_Report](
@SocialCategory int=0,
@AdmissionStatus int=0,
@Action char(2)
)
as
begin 
if(@Action='S')--to view
 Begin
	select SL,ApplicantName,Barcode,Gender,SocialCategory as SocialCategoryName,
	case AdmissionStatus
	when 0 then 'Pending'
	when 1  then 'Admited'
	when 2 then 'Rejectd'
	when 3 then 'Absent'
	else 'Not In List'
	end as admissionType,'M.P.Ed' as Course
	from T_Sports_MeritList_FinalNew_MPED M inner join T_Sports_Applicant_GeneralInfo_24022021 G on M.Barcode=G.vchApplicationNo
	where ListId=1 and (AdmissionStatus=@AdmissionStatus or  @AdmissionStatus=0)
	and (G.intSocialCategoryID=@SocialCategory or @SocialCategory=0)
 End
 end
